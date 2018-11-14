# MY NOTES

> NOTE: Don't treat this document as Wiki of some kind. These are my personal notes to problems I encountered or questions I asked myself during this repository preparation. They may not strictly refer to the repository itself, php or docker. Pleas note also that informations here provided, may not be true and some concepts I described here, might have been miss understood by me therefore I kindly suggest you to do reaserch on your own.

### Where to keep scripts to run them globally?
 - if these scripts are dedicated to a user: `$HOME/bin`
 - if these scripts are for everyone: `/usr/local/bin/`
 > NOTE: dont use `/usr/bin`, `/sbin`, nor `/bin`. These directories are dedicated for package-managed executables

### How does xDebug work?
When client initializes request (browser, cli, etc..) it sturts up php process (simplifying). If xDebug extension is on and is configured to run (by incomming connection or everytime) it behaves as a CLIENT to the DEBUGGIN SERVER (which f.e. sets up breakpoints). Therefore IDE must be properly set up as debugging server which listens on specified port, IP address and **server name**. If debuggin server does not respond and the client (debugger) cannot connect to the server php process runs debugging the script and slowing it down but does not provide interaction.<br>
Server Name - Specifies project. IDE is seen from within any container via the same IP (docker gateway) and debugger listens on same port.

### How does docker connect to IDE (or any other local/host or remote content)?
Every request originating from docker container goes throug **docker gateway** which is created by docker itself as host network interface which defaults to: `172.17.0.1`. It means that from within container every resource outside container boundaries is accesible **via** docker gateway.

### Why is `dockeruser` created for container?
Every user uid within container boundaries if matches host user uid is treated by system as **the same user**. Default root uid in linux system is set to `0`. If both container root user and host root user uid is set to `0` (which is by default) root user within contaner boundaries **is the same root user** as on host machine. Therefore container root user is granted god powers on host system.

### Basic knolege of PHP extensions

#### Summary
1. To install php extension you need lib dependency and its dependencies (f.e. zlib liblary)
1. To install php extension itself you need to download it from repostiory (like apk for alpine distro) or compile it yourself.
1. To enable the extension you need to configure php.ini file or create additional extension.ini file that is being loaded automaticly after php.ini is loaded.

#### More detailed description
- Extensioning with package manager (like apk or apt)
    1. Downlad extension for specified php version (like php7.2-zip)
    2. Every liblary dependency and its dependencies will be automatically (if not missing in package) downloaded and ready to use.
    3. Some packages are able to override or add .ini files and after installation the extension is automatically enabled and ready to use by php.
    4. If compiled php ext does not exist in repo (like at the moment php7.2-zip in apk, unlike php-zip) you need to compile it yourself.
- Extensioning with source code
    1. You need source code of your php version
    1. You need to download all extension dependency libraries and its dependencies manually. Remember to download them for development purposes (because you need to use them to compilation) so add -dev appendix (like zlib-dev)
    1. You need to compile it yourself (which is thankfully automated by official php docker image docker-php-ext-install script)
    1. Enable it in .ini file (thankfully script does it for us)
    1. Remove all junk (not done in this image)

### Offical PHP image helper scripts
1. `docker-php-ext-configure` - provides help with configuration when manual and custom compillation (of raw liblary (?) - not sure) is needed. Args that it receives are defined by compilation args themself
1. `docker-php-ext-install <lib-name>` - installs and compiles php extension using downloaded liblary and php version source codes. In this image it was used to create php7.2-zip ext using php source files in /php/src and zib liblary (zlib) with -dev appendix: zlib-dev.
1. `docker-php-ext-enable <php-ext-name>` - enables downloaded php-ext-name extension. It was used after xDebug extension isnstallation via pecl

#### SOURCES:
 - [Where to keep global scripts](https://askubuntu.com/questions/465109/where-should-i-put-my-script-so-that-i-can-run-it-by-a-direct-command)
 - [Where to keep user's scripts](https://askubuntu.com/questions/465109/where-should-i-put-my-script-so-that-i-can-run-it-by-a-direct-command/465113#465113)
 - [How does xDebug work](https://xdebug.org/docs/all#communication)
