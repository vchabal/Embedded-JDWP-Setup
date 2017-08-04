# JDWP Setup
## 1. Prepare Server
### 1.1 Setup EJDK
Download [Oracle Java Embedded], extract archive, and build JRE on your local machine according to [Java SE Embedded Guide]. It will create folder which will have *~50MB*.
```
># bin/jrecreate.sh --dest ./ejre-8 --ejdk-home ./ -g -x nashorn
># tar -czf ejre-8.tar.gz ./ejre-8
```
Upload `ejre-8.tar.gz` to server. Backup existing JRE and extract new content to existing JRE directory.
```
># tar -czf ejre-8.bak.tar.gz /opt/ejre-8
># tar -xzf ejre-8.tar.gz -C /opt/
```
### 1.2 Setup Java Debug Wire Protocol
On [JDWP Guide] you can find more details about setup. Add following line to script where you start the project.
```bash
ARGUMENTS="$ARGUMENTS -Xdebug -Xrunjdwp:transport=dt_socket,address=8888,server=y,suspend=y"
```
### 1.3 Restart Server
To apply changes, the server needs to be restarted. 
Make sure that your app is running after server restart.
```
># reboot
```
## 2. Connect with Eclipse to debug remotely
Setup your [Eclipse Remote Debug] with following settings, and press apply and debug. 
* Type **Standard(Socket Attach)**
* Properies **SERVER_IP_ADDRESS:8888**
* Check **Allow termination of remote VM**
* In Common tab check **Debug**

Open debug perspective, to **Edit Source Lookup**, or **Disconnect** and stop debugging.

[//]: # (Reference Links)
[Oracle Java Embedded]: <http://www.oracle.com/technetwork/java/embedded/overview/index.html>
[Java SE Embedded Guide]: <https://docs.oracle.com/javase/8/embedded/develop-apps-platforms/jrecreate.htm>
[JDWP Guide]: <https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/introclientissues005.html>
[Eclipse Remote Debug]: <https://dzone.com/articles/how-debug-remote-java-applicat>
