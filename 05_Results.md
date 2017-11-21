# Results
After running the Composition, the "Results: Detailed" dashboard will show up in the UI. This gives all transaction details and is useful for debugging purposes. To look for aggregate data there are other interesting dashboards like "Load Test" which gives an better overview of the whole test.

Using the "Dynamic Ramp" dashboard allows increasing the number of virtual users dynamically while the load test is running.

For checking the errors when the application is hit in a detailed way, the "Error Analysis" dashboard could be used.

Another useful is "Tables" type of dashboards (either grouped or hierarchical). This will show every component played in the clip with timers related to each of the calls made like Number of Collections Completed, Avg, Min and Max Duration, Std. Deviation, 90th Percentile, Bytes Sent and Received, Errors.

There are dashboards that allow showing the values of custom properties like the "Property Value Analysis" for Clip and Composition elements. In order to show this, the relevant custom property need to have the checkbox "Save value for analytics" selected.

For trobleshooting problems during a failed composition, check the "Event Log" dashboard.

Results can be exported with the purpose of importing into another reporting tool.

There are several formats supported
  * SOASTA XML
  * XML spreadsheet
  * CSV
  * RSS 2.0

### Reports
You can create an HTML or Word Document formatted report out of the results by right clicking and select "Create New Report". These hard-coded reports were initially used by Professional Services consultants to show a report to the customers about the results of load test scenarios. It is now available to customers. This functionality uses a different servlet inside the "Main" instance (selenium engine)
