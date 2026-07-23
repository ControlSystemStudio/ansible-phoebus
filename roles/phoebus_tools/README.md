Phoebus
=======

Build and install core Phoebus libraries.

Task Layout
-----------

- `tasks/main.yml`: orchestration entrypoint
- `tasks/build_phoebus.yml`: checkout and build core Phoebus

Role Variables
--------------

| Variable                                     | Type   | Description                                                                 |
|----------------------------------------------|--------|-----------------------------------------------------------------------------|
| `phoebus_tools_version`    | string | Phoebus upstream git branch/tag/commit                                     |
| `phoebus_tools_settings`   | string | Path to Maven settings file used by the build tasks                        |
| `phoebus_tools_override_mvn_settings` | bool | Render role-provided Maven `settings.xml` at `phoebus_tools_settings` |
| `phoebus_tools_build_always` | bool | Build even when git checkout reports no changes                             |

Dependencies
------------

- `phoebus_dependencies`

This role expects Java and Maven paths provided by `phoebus_dependencies`.

Author Information
------------------

Kunal Shroff <shroffk@bnl.gov>
