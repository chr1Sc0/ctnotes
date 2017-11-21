# Architecture
CloudTest is mostly a Java-based application that runs in Jboss Application Server. The are some additional software packages that integrate CloudTest for specific features. Software packages are normally installed in ""/usr/local" location.

https://community.akamai.com/docs/DOC-8834-architecture

### Components
There are several web services that give CloudTest each functional part:

  * **Maestro:** This is the service that plays the compositions. Is part of the CT Main instance and LG as well
  * **Repository:** This service is the endpoint for other services to be able to talk to the repository database. Could be installed separate from the Main CT instance.
  * **Results:** This is the service endpoint for the results database. Could be installed separate from the Main CT instance.
  * **Coordinator:** This is the endpoint service that Conductor or scommand uses to coommunicate with CT.
  * **Monitor:** Collects monitoring information
  * **ExternalData:** This allows integrating external sources like third-party monitoring applications (e.g: Amazon CloudWatch, New Relic, etc.)
  * **Collector:** Collects and consolidates the reports.
  * **Reporting:** Contains the service for generating HTML and Word reports.

The "soasta.ear" application package contains all the services mentioned above. This is the application deployed on Wildfly on the Main CloudTest instance. On the other hand, the "mastro.war" is the application deployed on the Maestro Load Generator instances and only contains the "Maestro" and "Monitor" services.

https://community.akamai.com/docs/DOC-8625-cloudtest-components

### JBoss Application Server (WildFly)
CloudTest version 58 is mainly based in Jboss Wildfly Application Server version 10.x. Previous versions used JBoss AS version 4.x. The relevant log is located in `"/usr/local/wildfly/log/server.log"`. Starting with CT version 58, Jboss runs within a docker as a containerized service. The `"/etc/init.d/jboss"` script wraps up all the docker commands to pull for the image from the docker repository and run the container.

### Database
The repository and results database used is PostgreSQL 9.x. The logs are located in `/vol/pgsql/9.0/data/pg_log/postgresql-<date>-<time>.log`

### Update Command Exexutor
The updatescommandexecutor provides a way to remotely execute commands on the Maestro settings after and upgrade for updating remotely the Maestro instances

### Selenium
The selenium component is responsible for creating the reports. The selenium server uses firefox in the background to generate the reports. If Firefox is upgraded in the CT instance, selenium has to be upgraded too to the last version (single jar file `selenium-server.jar`)

An X server is needed in order for Firefox to start as it needs a display where to redirect the output. Once firefox is started, selenium is able to generate the reports.

### Proxy Servers
For on-premises installations is important to make sure communication can happen when it involves proxy servers with the Licensing Server:

  1. Everytime the user logs in (to check the license validity)
  2. Every time a composition is started and ends.
  3. Every time a results is created.

Proxies can be configured in Settings -> Site Administration. Maestro instances do not use this general settings to talk to the CT Main instance. If a proxy it's needed from the LG Maestro instance, this is configured in the Server Settings (HTTPProxy setting)
