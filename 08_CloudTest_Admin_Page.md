# CloudTest Admin Page
It's a Webmin-based portal (Perl) for administering the Cloudtest server instances:

  1. Runs on port 10000
  2. The user "ctadmin" has permissions to access (password: "SOASTAadmin2006")
  3. It's only installed in on-premises installations.
  4. It gives basic monitoring information of memory and disk usage.
  5. Allows shutting down or rebooting the machine.
  6. Backup and restore the database (postgres).
  7. Download server logs (postgres logs and JBoss Wildfly logs)
  8. Change network settings

Time sync is important as the download of images from the docker repository requires the time to be in sync. Also alignment between the Main Cloudtest and the Load Generators for the dashboards to show properly.
