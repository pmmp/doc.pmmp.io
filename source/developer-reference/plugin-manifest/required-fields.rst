.. _plugin_yml_spec_required_fields:

Required fields
~~~~~~~~~~~~~~~


name
----

Type: ``string``

Name of the plugin. This may contain letters, numbers, hyphens, periods and underscores. It may also contain spaces, but this is discouraged.

version
-------

Type: ``string``

Self explanatory. It's recommended to use a 3-point semantic version, but this can be anything you like.

main
----

Type: ``string``

Fully-qualified name of the main class. This class must meet the following criteria:

- MUST NOT be abstract
- MUST implement the ``pocketmine\plugin\Plugin`` interface

api
---

Type: ``string`` or ``string[]``

The API version(s) that the plugin is compatible with. If the plugin's API version is not compatible with that of the server, the server will refuse to load the plugin. More info on API versioning can be found `here <api_version_spec>`.
