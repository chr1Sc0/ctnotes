# Automating Tools

### Scommand

Client-side Command Line Interface (CLI) that can be used to interact and automate tasks in CloudTest.
It's Java-based (jar file) that it's downloaded to the client. It requires Java SDK to be installed in the client.

An scommand reference can be found here:
https://community.akamai.com/docs/DOC-9060-scommand-reference

The help is comprehensive and context-based.
```
/opt/local/scommand/bin/scommand help
Command-line client (build 9569.393).

Usage: scommand cmd=<subcommand> [args]

Available commands:
  delete   Deletes a Repository object.
  drain    Sets the   username=USERNAME     : User name
 password=PASSWORD     : Password
 apitoken=APITOKEN     : API Token
 url=URL               : URL
 httpproxyhost=SERVER  : HTTP proxy server name (optional)
 httpproxyport=PORT    : HTTP proxy port (optional)
 sockettimeout=TIMEOUT : Socket timeout (optional)
 connectiontimeout=TIMEOUT : Connection timeout (optional)
 keystore=KEYSTORE     : Path to client key store (optional)
 keystorepass=PASSWORD : The password for the client key store (optional) services to "drain" mode.
  export   Exports a Repository object to XML format.
  help     Displays this help.
  import   Imports Repository objects from a file (or list of files).
  list     Displays a list of Repository objects.
  play     Plays a composition or playlist.
  rename   Re-names a Repository object.
  start    Starts a monitor.
  status   Displays the current status of the services.
  start-env Starts a Test Environment
  terminate-env Terminates a Test Environment
  start-grid Starts a Grid
  terminate-grid Terminates a Grid
  start-rsdb Starts a Results Database
  terminate-rsdb Terminates a Results Database

Common parameters (used by all commands):
 username=USERNAME     : User name
 password=PASSWORD     : Password
 apitoken=APITOKEN     : API Token
 url=URL               : URL
 httpproxyhost=SERVER  : HTTP proxy server name (optional)
 httpproxyport=PORT    : HTTP proxy port (optional)
 sockettimeout=TIMEOUT : Socket timeout (optional)
 connectiontimeout=TIMEOUT : Connection timeout (optional)
 keystore=KEYSTORE     : Path to client key store (optional)
 keystorepass=PASSWORD : The password for the client key store (optional)
```

Type scommand help <subcommand> for help on a specific subcommand.

Example:
```
/opt/local/scommand/bin/scommand cmd=list type=composition username=cscotti password=*** \
                                 url=https://172.29.26.73:8443/concerto
/cscotti/Composition for soastastore recording at 10-27-2017, 11:20:21 AM clip
/cscotti/Composition for soastastore recording at 10-27-2017, 11:20:21 AM clip/Draft of Composition for soastastore recording at 10-27-2017, 11:20:21 AM clip created on October 30, 2017 10:40:23 AM UTC
2 object(s) found.
```
### Jenkins
Jenkins is a self-contained, open source automation server which can be used to automate all sorts of tasks related to building, testing, and deploying software.

#### Jenkings Plugin
Jenkins can be installed through native system packages, Docker, or even run standalone by any machine with a Java Runtime Environment (JRE) installed.

The CloudTest Jenkins plugin provides the ability to
  1. Easily run the MakeAppTouchTestable utility on an iOS or Android project
  2. Silently install an iOS app on a connected device
  3. Play CloudTest compositions and include the output in the build's test results
  4. Launch and tear down grids, results databases, and test environments

What the Jenkins plugin does in the background is simply execute scommands to CloudTest.

If the Jenkins server has multiple versions of Java JRE and the default Java version is 1.6, it will cause the scommands to fail as scommand is able to work with JRE 1.7 and above.
