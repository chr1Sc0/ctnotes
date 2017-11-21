# Troubleshooting

### Conductor
To check the Conductor log file, select from the menu -> Help -> View log contents (in the user profile folder)

For HTTPS, the Conductor adds it's own certificate to the PC key-store.  For SSL connections recording, it's needed to have this certificate loaded as the browser will be connecting to an unknown certificate authority. For this reason,loading this SOASTA CA certificate in the machine certificate store as a trusted authority is needed.

### Compositions
Check the "Event Log" results Dashboards

### On-premises Main Instance
The main log to check in case of a problem would be the Jboss log:
`"/usr/local/wildfly/log/server.log"`.

The `"/etc/init.d/jboss"` wrapper script could be use to restart Jboss:

`/etc/init.d/jboss stop`
`/etc/init.d/jboss start`

### Proxies
For troubleshooting connectivity through proxies, it could be useful to verify in the Maestro instance using "curl" to connect to "cloudtestmanager.soasta.com", e.g:
`# curl [-k] https://licensing.soasta.com/concerto/central -v --proxy <proxy_IP:proxy_port>`

### Cloud-based Main
It's possible to SSH the main instance, the outgoing IP needs to be allowed in the "Security Group" attached to the instance. The credentials for support are:

support/ManillaFallstoUS1945

If there's a problem deploying the instance and it keeps failing when doing the server checks and continously destroys and recreates the instance, the following log would be relevant to check for errors:
`/var/log/ec2_install_cloudtest.log`

For the installation of CloudTest, the following log could be of use:
`/var/log/cloudtest_install.log`
