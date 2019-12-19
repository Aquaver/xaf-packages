# Example Package

This XAF Package Manager package is an example application which shows general working of XAF PM. It allows the user to learn how to manage custom packages by installation, checking for possible updates (this package probably will not be updated, but no for sure), updating to newer version and deinstallation. It comes with all essential files for all XAF PM standalone application, but with only one executable file - the index file. It is only for demonstrative purposes, therefore it will only print Hello World on run.

## How to install and manage

* **Installation** - `xaf-pm package [-a | -add] xaf-other/example-package-src`
* **Checking for updates** - `xaf-pm check [-p | --package] example-package-src`
* **Updating** - `xaf-pm update [-p | --package] example-package-src`
* **Deinstallation** - `xaf-pm package [-r | --remove] example-package-src`

**Important!** All packages on this repository comes with two versions - source (full) and minified (compressed). Therefore, all of them has either `src` or `min` trailing suffix. This example description concerns the source version of this package. If you would like to test it for the minified one, use `example-package-min` name. It is strongly recommended following this format on custom XAF package repositories, but is not obligatory to proper functioning.
