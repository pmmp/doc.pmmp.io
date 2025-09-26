.. _api_version_spec:

API versioning
--------------

PocketMine-MP plugins are required to declare which API versions they are compatible with. This is used to decide whether or not to load a plugin, and to gracefully degrade when the plugin is not compatible with the given server version.

As of PocketMine-MP 3.0.0, the API version is the same as the server version. This version is a semantic ``major.minor.patch`` version number. Read more about `semantic versioning <https://semver.org/>`_.


How the API version is changed
==============================

+-------+------------------+--------------------------------------------------------------------------------------------------------+
| Type  | Example          | Description                                                                                            |
+=======+==================+========================================================================================================+
| Major | 5.33.0 -> 6.0.0  | Changing or deleting features                                                                          |
+-------+------------------+--------------------------------------------------------------------------------------------------------+
| Minor | 5.33.0 -> 5.34.0 | New features were added, existing ones were deprecated, or the supported Minecraft version was changed |
+-------+------------------+--------------------------------------------------------------------------------------------------------+
| Patch | 5.33.0 -> 5.33.1 | Bugs were fixed                                                                                        |
+-------+------------------+--------------------------------------------------------------------------------------------------------+


Compatibility checking examples
===============================

+----------------+----------------+------------+---------------------------------------------------------------------------------+
| Server version | Plugin version | Compatible | Reason                                                                          |
+================+================+============+=================================================================================+
| 4.0.0          | 3.0.0          | NO         | Major versions are different.                                                   |
+----------------+----------------+------------+---------------------------------------------------------------------------------+
| 3.1.0          | 3.0.0          | YES        | Server has a greater minor version than the plugin, guaranteeing compatibility. |
+----------------+----------------+------------+---------------------------------------------------------------------------------+
| 3.0.0          | 3.1.0          | NO         | Plugin requires new features not found in the given server version              |
+----------------+----------------+------------+---------------------------------------------------------------------------------+
| 3.0.1          | 3.0.0          | YES        | Server has a greater patch version than the plugin, guaranteeing compatibility. |
+----------------+----------------+------------+---------------------------------------------------------------------------------+
| 3.0.0          | 3.0.1          | NO         | Plugin requires newer bug fixes not found in the given server version           |
+----------------+----------------+------------+---------------------------------------------------------------------------------+


How to choose your supported API version
========================================

You should choose the **minimum version that supports the things that you need**.

For example, if the feature you want was first added in ``3.1.0``, you can require ``3.1.0`` as a minimum even if the currently supported version is ``3.2.0``. This is to ensure that users get a smoother experience no matter what version of PocketMine-MP they are using.

Of course, you should test your plugin on your minimum version to make sure that everything works correctly. However, it may of course not make sense to require a lower version if the earlier versions are end-of-life.

Common pitfalls and misconceptions
==================================

- The API version **is not a magic number**. Changing it blindly **will not make a plugin magically work** on a version it wasn't designed for.
- It is **not required to write out every single compatible version** in your plugin's manifest. Only the **minimum required version of each major version** is required.

  - Good: ``[3.1.0]`` (single minimum version), ``[3.2.0, 4.0.0]`` (minimum version from two different major branches)
  - Bad: ``[3.1.0, 3.1.1, 3.1.2]`` - this is **not** desired and the superfluous versions will be ignored.

- Ensure that your plugin **actually runs on the versions you specified**. Versions which it a) crashes on, or b) doesn't work as expected, should be removed from your versions list.
