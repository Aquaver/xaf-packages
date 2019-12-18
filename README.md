<p align="center">
  <img alt="XAF Package Repository Logo" src="https://raw.githubusercontent.com/Aquaver/xaf-packages/master/_config/assets/logo.png"><br><br>
  <img alt="Required XAF" src="https://raw.githubusercontent.com/Aquaver/xaf-packages/master/_config/assets/versions/framework.svg?sanitize=true">
</p>

Welcome to Extensible Application Framework Package Manager - Default package repository. This is the place, where user could find some program packages that are ready to install via the XAF Packager Manager (PM) and use them. It is names 'default' because its path signature is predefined in PM source repository list and it cannot be deleted (via PM controller obviously) unlike the other repositories, added by the user. Because this is first XAF 'official' package repository, the minimum required API version is the oldest - 1.0.0 version. However, it only means that the repository will not force user to update XAF to later versions, but if one of user's choosen program has defined required XAF version later than default required by the repository, it will override this value in repository configuration. That is the one of few reasons of keeping XAF API up-to-date. Finally, it comes down to executing one controller's command, maybe possibly two.

## Program categories

To not let the entire repository fall into total chaos, all programs are not kept in one place together. Every add-on package must be assigned to specified one category. Categories are just subdirectories created in 'master' main category, next to repository configuration directory named `_config`. This also gives an opportunity to store packages with exactly the same name but they must be placed in different categories obviously. From the user's side, add-on category handling does not make downloading procedure more complicated, it comes down to specify package identifier as `category-name/package-name`. Furthermore, XAF Package Manager controller program has embed function to get the repository's category list. However, XAF PM standard repository structure provides that every program must be placed in category. Add-on package that is stored in repository main directory will not be detected. If you would like to create your own XAF PM add-on package repository, you could keep all programs in one category, just named 'all', but this is required to function properly.

## Standard repository and package structure

### Repository structure hierarchy

```
repository-name
   ├─ _config
   │   └─ repository.info (file)
   ├─ category-a
   │   ├─ program-a
   │   ├─ add-on-b
   │   └─ package-c
   ├─ category-b
   │   ├─ another-program-a
   │   ├─ xaf-add-on-b
   │   └─ package-c
   └─ category-c
       └─ ...
```

XAF Package Manager add-on repository structure standard provides a few rules and recommendations about creating custom source repositories. They are required in order to let the PM controller function properly without unexpected bugs and errors. The most important rule is the directory and *file tree layout* as shown above. First directory, named `_config` is a *repository configuration directory*, which contains main settings and repository description file, named `repository.info`. These names are constant, and must not be named in other way. Furthermore, it is strongly recommended all objects (directories and files) to have name in this format `lower-letters-with-hyphen-spacing` (with extension, if it is file obviously). However, this is not obligatory to fulfill this requirement, because XAF Package Manager will detect categories and packages names in other format. This is only a recommendation. Repositories also have not any limit of category and add-on package count, custom sources may have as lot of them as the GitHub service disk restriction allows. Moreover, XAF PM does not forbid the repository to have other files in its master directory than connected with general PM functionality.

### Package structure hierarchy

```
package-name
   ├─ _bin
   │   ├─ index.lua (file)
   │   ├─ my-program.lua (file)
   │   └─ program-data
   |       ├─ another-code.lua (file)
   |       └─ ...
   ├─ _config
   │   └─ package.info (file)
   └─ README.md (not required, optional)
```

XAF Package Manager add-on package structure standard does not deviate from the above rules very much, but there are little changes. Firstly, the structure hierarchy is a bit different - the package master directory has not one, but two fixed named subdirectories which has files inside them - `_bin`, which stores all user program data and executable files, literally everything, the program needs to run. The second one is - `_config`, which as same as PM package repository, contains package configuration data and description information. Secondly, in constrast to repository structure, in add-on package directory, among these two main subdirectories and optional `README.md` file, **there should (or even must) not be other files and subdirectories** than these two (three) ones. On case of detecting unexpected files in package master category, the PM controller will return an information about it and **interrupts the installation** procedure.

## Repository and package configuration files

### Repository description data

```
[#] Extensible Application Framework add-on repository description data.
[#] This file is used to identify this repository in XAF Package Manager.
[#] Data represented in XAF Table Format.

[S] repository-description = [S] Extensible Application Framework Package Manager official default add-on package repository.
[S] repository-owner = [S] Aquaver
[S] repository-title = [S] XAF Package Manager - Default standard package repository.
[S] repository-xaf = [S] 1.0.0
```

Package repository configuration file generally contains descriptive information that are used in identification in XAF Package Manager. As it concerns standard repository and package hierarchy structures, there are also some rules of storing specific data that may affect on the installation process. All these data are saved in XAF Table Format and are processed by XAF Core class. That is the one of reasons, why XAF is needed to run the PM controller. Above file fragment is that configuration file of `xaf-other/example-package` add-on, and presents the structure of this file type. First three lines are marked as `[#]` - comments, and they may be removed without any consequences, if you would like to. First data line is named `repository-description` - it is just a repository description as its name says. This description may be plain sentences without any limit, but must fit in one line without line-breaks. The next line is named `repository-owner`, just a nickname or full name of the repository's owner (author). Another line, named `repository-title` is a name that is shown in Package Manager contoller while getting repository information by it. Also could be plain sentences with spaces. But the last line is more important than previous ones. The configuration value called `repository-xaf` is the XAF (not PM) version that are required by **all packages on this repository** forced during installation. If the user has older XAF version, the repository will deny further installation and aborts it.

### Package description data

```
[#] Extensible Application Framework add-on package description file.
[#] This file is used to identify this project in XAF Package Manager.
[#] Data represented in XAF Table Format.

[S] package-description = [S] This is example package, which shows basics of XAF PM functionality and general working.
[S] package-identifier = [S] example-package
[S] package-index = [S] index.lua
[S] package-owner = [S] Aquaver
[S] package-title = [S] XAF Example Package
[S] package-version = [S] 1.0.0
[S] package-xaf = [S] 1.0.0
```

Add-on package configuration file as the previous one, stores description about it to help XAF Package Manager in identifying this project in entire repository. It is also represented in XAF Table Format, and it consists of a few configuration entries. Like in repository configuration file, the first three lines are comments and they are not required to store this data properly. Fifth line, as its name says - `package-description` stores general add-on description, which tell the user what the project does, it may be written in plain sentences with spaces. But the next line - `package-identifier`, is very important, because it may affect on whole installation process. It is the package identifier, it **must be equal to directory name in repository** because otherwise, the installation process will be aborted. Another line is also quite essential, the value of `package-index` is a **relative path** of the index script - like in websites, index file is first script executed on program run via XAF PM controller. The next two lines, both `package-owner` and `package-title` work exactly the same as the repository's versions, only for informative purposes. Technically, `package-version` is also only a information for the Package Manager controller, it shows the user progress of project development, nothing else. The last one line - `package-xaf` works as same as in case of repository, it shows the minimum required XAF (not PM) version to run the package program. If the user has older version than this one, the PM controller will abort the installation procedure.
