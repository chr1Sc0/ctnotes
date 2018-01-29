
*CloudTest Manual Upgrade*

**Main Instance**

1.  Download the soasta.ear and concerto-client-apps.zip for latest CT version into your Main instance
2.  Copy the files to the Main instance
3.  Login as support user and su to root
4.  Stop JBoss:
    `# /etc/init.d/jboss stop`

5.  Unzip concerto-client-apps.zip, then run:
    # ./bin/migrate-repository-db
    # ./bin/migrate-resultsservice-db

6.  Copy the soasta.ear file to:
  a. CT >= 58: `/usr/local/wildfly/deploy`
  b. CT <= 57: `$JBOSS_HOME/server/cloudtest/deploy`

7.  Start JBOSS and confirm if Main is migrated successfully:
    `# /etc/init.d/jboss start`


**Maestro Instance**

1.  Download maestro.war file and copy into the Maestro instance
2.  Login as support user and su to root
3.  Stop JBoss:
    `# /etc/init.d/jboss stop`

4.  Copy the maestro.war file and rename into:
    a. CT >= 58: `/usr/local/wildfly/deploy/concerto.war`
    b. CT <= 57: `$JBOSS_HOME/server/cloudtest/concerto.war`

5.  Start JBoss and confirm you can do Check Server from Servers page CT UI:
      `# /etc/init.d/jboss start`
