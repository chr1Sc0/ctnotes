# Upgrading CloudTest

### Automatic Upgrade
Going to the "About" menus shows in the "Updates" tab the newer versions available for directly downloading and updating CT. This simply updates the EAR and WAR files in the CloudTest instances. It gets the packages from cdn.soasta.com which needs to be reachable from the customer site. If this is not reachable, the download will fail after a number of retries.

### Manual Upgrade
When the customer does not have outside access for automatic updates, a manual update is possible.

For upgrading Main instance you need to have:
  - File soasta.ear
  - File concerto-client-apps.zip (tools to upgrade the database schema)

FTP to get the files: ftp.soasta.com (user:customersupport/sierra)

The steps for manual upgrade:

1. Download the files from the new version from the FTP
2. Stop Jboss:
  # sudo /etc/init.d/jboss stop
3. Unzip concerto-client-apps.zip
4. Migrate the repository database (PG needs to keep running)
   # sudo ./concerto-client-apps/migrate-repository
5. Migrate the results database (PG needs to keep running)
   # sudo ./concerto-client-apps/migrate-resultsservice-db
6. Copy the nee soasta.ear to the deploy directory:
   # sudo cp ~/soasta.ear /usr/local/jboss-4.4.2.GA/server/cloudtest/deploy/soasta.ear
7. Start Jboss:
   # sudo /etc/init.d/jboss start

### Migrating from CloudTest version 57 to 58
For upgrading from 57 to 58, it's not supported an in-place upgrade as it involves a newer OS version, Java, JBoss, etc. Only a side-by-side upgrade is supported by copying the database from the 57 and the updating it.

The steps to migrate from 57 to 58 are these:

1. Install earlier version of CT 57.35 (http://cdn.soasta.com/cloudtest-isos/8744.687/cloudtest-main.iso?e=1509845931&h=8cc0167ea2068fe40ce903f2d310d297)
2. Shut down CT 58 to use the same license for 57
3. Create dummy compositions
4.  Shut down jboss in 57: /etc/init.d/jboss stop
5.  Zip the data folder: tar cvf data.tar /data/pgsql/9.0/data
6.  Scp the file to 58
7.  Shutdown jboss and postgres in 58: /etc/init.d/jboss stop and /etc/init.d/postgresql-9.0 stop
8.  Unzip the data file: tar xvf data.tar inside /vol folder
9.  Set the owner of the folder: chown –R postgres:postgres /vol/data
10. Move the 58 data folder: mv /vol/pgsql/9.0/data ~/old-data
11. Create sym link : ln –s /vol/data /vol/pgsql/9.0/data
12. Start postgresql-9.0 service: and /etc/init.d/postgresql-9.0 start
13. Upgrade the 57 database: /root/postinstall/pgsql/concerto-client-apps/bin/migrate-repository
14. Set the password for postgres user: psql template1 -U postgres -c "ALTER USER postgres WITH PASSWORD 'postgres'"
15. Upgrade 57 RSDB: /root/postinstall/pgsql/concerto-client-apps/bin/migrate-resultsservice-db
16. Start jboss: /etc/init.d/jboss start, CT 58 should now access the upgraded 57 data.

The license key will get suspended as it was being used with 57 and now it's being used from 58. As customers would want to have both instances running, support sends a temporary license for 58.

If the customer has a temporary license, it needs to be updated in the database before bringing the 58 instance up.

`# psql -U postgres -d soasta_repository`
`> select licensekey from siteconfiguration;`
`> UPDATE siteconfiguration SET licensekey = "<new-license-key>";`

Finally update the servers entries in the "Servers" page as these will have old IP addresses from the database.
