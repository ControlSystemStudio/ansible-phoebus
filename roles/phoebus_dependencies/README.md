# phoebus_dependencies

Install the Java and Maven toolchain required by Phoebus roles.

## Variables

- `phoebus_dependencies_jdk_versions`: list of JDK versions and archive URLs to install
- `phoebus_dependencies_maven_version`: Maven version to install
- `phoebus_dependencies_maven_url`: Maven archive URL
- `phoebus_dependencies_account`: owner/group used for installed files
- `phoebus_dependencies_root`: installation root for shared dependencies

## Installed layout

- `${phoebus_dependencies_root}/jvm/jdk-<version>`
- `${phoebus_dependencies_root}/apache-maven-<version>`
