.. _threading_in_php_wtf:

Threading in PHP - WTF?
-----------------------

This page aims to give some technical insight into what's required to get threading in PHP, and why every threading extension for PHP sucks.

PHP is not designed for this!
=============================

PHP's design goal is to provide an easy scripting language for use on webservers, for delivering webpages to browsers. It's popular for this use case. Unfortunately, web requests don't usually need threading in user code, since web requests typically last a few seconds at most, and are mostly I/O bound, not needing the use of many CPU cores. PHP has flourished for over 20 years without support for user threads, and it's likely this will continue to be the case for years to come.

Because almost all use-cases for PHP involve serving web requests, the design choices made by the PHP developers over the decades have been oriented with a webserver-first approach. Serving webpages is something PHP does very well. One of these design choices has been to make no effort whatsoever to implement support for userland threading.

Almost everything must be copied
================================

Every complex data structure in PHP is non-thread-safe. This applies to userland types such as arrays, objects, strings, and resources, and also applies to things you might not expect - functions, classes, and constants. Reference counts on these data structures are not atomic, and the Zend Engine's memory manager goes out of its way to prevent stuff from being shared between one thread's memory manager and another.

This means **all of these things must be copied** in order to get them from one thread to another, which makes passing large data from one thread to another very expensive, and therefore **severely limits** the viable use cases of PHP threading. The CPU cost of copying the required data onto the target thread can easily exceed the time saved by threading.

The only viable use cases are those which require relatively **little transfer of data** between threads but have relatively **large time cost**. Currently, PocketMine-MP only uses threads for world generation, light calculation, network compression, some internal network systems, and the occasional cURL request.

Threads don't inherit anything
==============================

Every new thread in a ZTS build of PHP gets a completely new interpreter context. This means that no user classes are loaded (unless `preloaded by OPcache <https://www.php.net/manual/en/opcache.preloading.php>`_).

Classes and functions aren't shared (or shareable) between threads, and therefore must be copied, or otherwise reloaded, onto a new thread.

Code to copy class and function data structures from one thread to another makes up the majority of code in PHP threading extensions such as `pthreads <https://github.com/pmmp/pthreads>`_ (and therefore the majority of the bugs).

Other extensions such as `parallel <https://github.com/krakjoe/parallel>`_ reduce complexity by forcing the use of autoloaders to reload classes on new threads instead of copying them, but this imposes some limitations, since not all stuff can be autoloaded (e.g. anonymous classes). In addition, it still needs to be able to copy functions (since its unit of work is a closure).

To make matters worse, these internal data structures are subject to change from one PHP version to the next, meaning that this code often breaks, and is the main obstacle to upgrading PHP version in projects like PocketMine-MP.

ZTS (Zend Thread Safety)
========================

The Zend Engine at the heart of the PHP interpreter provides two modes of operation.

- NTS (Non Thread Safe) makes up the vast majority of PHP installations. In this mode, there may only be one interpreter context in a process. Thread safety is not usually needed in a typical PHP use-case, since a webserver just spins up a new PHP process for each request.
- ZTS (Zend Thread Safe) is used to allow each webserver request to run in a new thread of the same process, rather than in a separate process. Each thread has its own independent interpreter context. This mode is typically used on Windows, where `fork(2) <https://www.man7.org/linux/man-pages/man2/fork.2.html>`_ is not available.

Neither of these modes is suitable for user threading. NTS is (obviously) not thread-safe, so accessing global state on different threads at the same time would lead to data races and possibly crashes.

ZTS is marginally less unsuitable. While ZTS enables running multiple independent threads of PHP code in the same process, it does so by making sure that each thread can't access any state from other threads. This is great for webservers, where different requests shouldn't be able to interfere with each other, but it's a big obstacle for userland threading, where interaction between different threads is necessary.

Every threading extension made for PHP has built on top of the ZTS mode, and from there done an enormous amount of hacks to make different threads able to interact with each other, despite the limitations imposed by the Zend Engine.

Implementing threading properly into PHP would require a significant amount of changes to the PHP core, which it seems no one in the world is inclined to do. Until the time comes when a knight in shining armour implements threading properly into PHP, we're stuck with stuff like pthreads and all the hacks necessary to make it even remotely usable.
