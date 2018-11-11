# MY NOTES

### Where to keep scripts to run it globally?
 - if these scripts are dedicated to a user: `$HOME/bin`
 - if these scripts are for everyone: `/usr/local/bin/`
 > NOTE: dont use `/usr/bin`, `/sbin`, nor `/bin`. These directories are dedicated for package-managed executables

### How does xDebug work?
When client initializes request (browser, cli, etc..) it sturts up php process (simplifying). If xDebug extension is on and is configuret to run (by incomming connection or everytime) it behaves as a CLIENT to the DEBUGGIN SERVER. Therefore IDE or/and docker container must be properly set up as debugging server which listens on specified port and IP address. If debuggin server does not respond and the client (debugger) cannot connect to the server php process runs without debugging the script.

 #### SOURCES:
 - [Where to keep global scripts](https://askubuntu.com/questions/465109/where-should-i-put-my-script-so-that-i-can-run-it-by-a-direct-command)
 - [Where to keep user's scripts](https://askubuntu.com/questions/465109/where-should-i-put-my-script-so-that-i-can-run-it-by-a-direct-command/465113#465113)
 - [How does xDebug work](https://xdebug.org/docs/all#communication)