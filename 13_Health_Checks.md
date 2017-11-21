# Health Checks
There are a number of settings that define thresholds for CPU and Memory usage. These values are used to identify when the instance is getting stressed while running heavy scripts during instensive load testing. Once a particular threshold has been crossed, the Composition will get terminated and the test would stop playing:

Normally, the Load Generators (Maestor) are the instances that suffer the most when doing such intensive tests. The settings below are specially meaningful for the the Mastro instances:

  * **Monitor.FreeMem.Threshold:** Percentage of free memory needed for the test to continue (3% default).
  * **Monitor.LoadAvg1MinThreshold:** Number of threads that could be in "WAITING" or "BLOCKED" status for 1 min period (default: 50 per core)
  * **Monitor.LoadAvg2MinThreshold:** Number of threads that could be in "WAITING" or "BLOCKED" status for 2 mins period (default: 25 per core)
  * **Monitor.LoadAvg5MinThreshold:** Number of threads that could be in "WAITING" or "BLOCKED" status for 15 min period (default: 15 per core)
  * **Monitor.LoadAvg15MinThreshold:** Number of threads that could be in "WAITING" or "BLOCKED" status for 15 min period (default: 5 per core)
  * **Monitor.UnhealthyAction:** "STOP" to finish the full test or "DRAIN" to finish the current action and then stop the test.

The Results service does not get stressed that often but could happen that performance slows down significantly. The following settings might be relevant under such events:
  * **HealhCheck.Database.Max.Problem.Percent**
  * **HealthCheck.FreeMem.Threshold**

All these Healthcheks could be disabled by setting them to "-1"

The "Event Log Dashboard" from the Results to know if a health check threshold has been passed and a composition was stopped due to this reason.

For more info about health check settings:
https://community.akamai.com/docs/DOC-8671-cloudtest-health-settings
