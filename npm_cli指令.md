### Package management
npm i - install缩写
npm install	- 安装package.json里面的内容
npm install --production	- 安装package.json里面除了devDependecies的内容
npm install package-name	- 安装package-name
npm install --save-dev lodash	- devDependency中安装package-name
npm install --save-exact lodash	- Install with exact
--save is the default as of npm@5. Previously, using npm install without --save doesn’t update package.json.

### Install
npm i sax	NPM package
npm i sax@latest	Specify tag latest
npm i sax@3.0.0	Specify version 3.0.0
npm i sax@">=1 <2.0"	Specify version range
npm i @org/sax	Scoped NPM package
npm i user/repo	GitHub
npm i user/repo#master	GitHub
npm i github:user/repo	GitHub
npm i gitlab:user/repo	GitLab
npm i /path/to/repo	Absolute path
npm i ./archive.tgz	Tarball
npm i https://site.com/archive.tgz	Tarball via HTTP

### Listing
npm list	- Lists the installed versions of all dependencies in this software
npm list -g --depth 0	- Lists the installed versions of all globally installed packages
npm view	- Lists the latest versions of all dependencies in this software
npm outdated	- Lists only the dependencies in this software which are outdated

### Updating
npm update	- Update production packages
npm update --dev   - Update dev packages
npm update -g   - Update global packages
npm update lodash	- Update a package

### Misc features
npm owner add USERNAME PACKAGENAME - Add someone as an owner
npm ls - list packages
npm deprecate PACKAGE@"< 0.2.0" "critical bug fixed in v0.2.0" - Adds warning to those that install a package of old versions
npm update [-g] PACKAGE - update all packages, or selected packages
npm outdated [PACKAGE] - Check for outdated packages

参考文档：
1. https://devhints.io/npm
2. https://docs.npmjs.com/cli-documentation/cli
