# Installation
The on-premises version of CloudTest is an appliance provided through an ISO image. This ISO image is downloaded from the central CloudTest Manager instance hosted on Akamai insfrastructure in this URL: https://cloudtestmanage.soasta.com

To download, you have to login and follow these steps:
  1. Go to the the "Builds" page on the left pane
  2. Right Click over a specific build
  3. Select the option "Generate ISO"
  4. Choose the number of dats for the URLs to be available and click "Generate"
  5. Download the ISO images from the provided URLs

It's a Linux (CentOS) installation image that comes with all the CloudTest software pre-installed. The minimum hardware specs for a small CloudTest Main instance testing installation are:
  * 4 CPU
  * 4GB RAM
  * 40 GB Disk

The installation ISO will request what type of CloudTest image to install:
  * **Main:** Main CloudTest image
  * **Maestro:** Load Generator image
  * **Consolidator:** Instance where results from Maestro images get consolidated
  * **Results Database:** In case the database is run separated from the Main instance

The root user is restricted. For elevated permissions, the "support" user can be used but the password is not given to customers.

### Licensing Server
Once the installation finishes, every CloudTest installation will need to verify its license against [CloudTest Manager](https://cloudtestmanager.soasta.com). The "Licenses" pane contain all license keys issued for each CloudTest instance. If a new instance is installed and tries to use a key that has been already issued and activated, this will set the "account status" to suspended. Each license is bound to the mac address of the installation, hence to the machine where the installation has been performed. This is to avoid users using the same key for multiple instances.
