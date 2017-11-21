# Servers
The "Servers Resources" page is where the CloudTest main instance can manage the load generators, consolidators and Results Database instances added.

### Maestro Load Generator (Test Server)
Load Generator instances launch the compositions that are sent to the target for load testing. This allow scaling up the test and use several locations worldwide. Every instance can approximately carry a load of 100-300 Virtual Users depending on the resources of the hardware in use.

For more info about adding Load Generator instances:
https://community.akamai.com/docs/DOC-8381-setting-up-server-lists-load-generators-v11pdf

### Adding Servers
First we need to add one location in the "Locations" object. This is simply a logical container that is used to group "Servers". Once the Location is added, we can add the Main CT server instance and LG instances.

For the main instance server type, all the services are available:
  - Maestro
  - Repository
  - Results
  - Coordinator
  - Monitor
  - ExternalData
  - Collector
  - Reporting

The Load Generator does not have the UI service but just the following services:
  - Maestro
  - Monitor

Internal and external access URLs can be specified in case the instance is in the cloud and the exposed public IP is different from the internal IP. If the Location where the Main instance and the Maestro instances is different, the external IP address will be used instead of the internal IPs. This is useful for the Cloud-based load testing where the instances could be in different regions or availability zones.

### Check Servers
After adding the services URLs, the "Check Server(s)" tab can be used to verify that all services are reachable. This check would only do a check to verify the Main instance can reach the LGs but does not check if the connectivity in the other direction. For checking the other direction, the "Player Status" in the Activity item can be used.

For more info about using servers, check:
https://community.akamai.com/docs/DOC-8771-using-servers
