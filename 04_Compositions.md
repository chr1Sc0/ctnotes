# Compositions
The Composition is the test itself that will be played and contains one or more clips arranged on tracks and governed by user-specified sequence and tempo. By using simultaneous tracks, defining virtual users, repeats, and locations; and by specifying repeats on tracks and clips you can build powerful, multi-user tests.

There are different hierarchy levels to control de flow of the composition:

Composition -> Band -> Track -> Clip

For a description of the task flow to create a Composition, check:
https://community.akamai.com/docs/DOC-8933-creating-new-compositions

With "Enable Repeat -> Repeat Type" set to Parallel and then setting the number in "Repeat by" we can define how many Virtual Users (VUs) will run in parallel. It's also important to set "Minutes to Ramp Up" to define the interval to gradually increase the number of VUs over time instead of starting with all at the same time.  With "Renew Parallel Repeats" once the clip is finished, it will start again in a cyclic way until the user manually stops the test.

To start the test, click "Play" and then it will show the "Results" dashboard with the live results as the composition runs.

Saved compositions can be exported and imported from different instances of CloudTest.

When running compositons, there are two possible modes:
  1. General
  2. Load

In "General" mode, all the details are logged in the results like headers, body, response data of the request, etc. In "Load" mode, not all details are logged but just aggregate data.

### Locations
When editing the composition, the Track General settings has a few options available for the "Location" setting:

1. General Servers
2. Load Server
3. Dedicated Servers
4. Locations
5. Servers at \<Location>

The "Location"  defines where to run the clip from. It shows all the available servers to select that have been added in "Servers". Setting "Any Location" would go to the CT main instance.  If there are multiple servers at a specific location and the location is selected, it will use the first LG with "Idle" status.

In the "Activity" page, it's possible to determine the active/idle Load Generator instances and which compositions are running.

> **Caveat:** Choosing "Load Server" will make the compositio unless the "Maestro" service has the "ServerType" property defined to "Load" (the default value is "General") in at least one server instance. The "General" type allows running multiple compositions from the same server. This is OK if the composition does not have a high number Virtual Users.

If there's a high number of parallel virtual users, it's appropriate to change the server type to "Load". This makes the LG server to run just one composition at a time.

The difference between "Load Server" and "Dedicated Load Server" is that the first one can run one composition at a time while the second one can run just one track of one composition at a time. If the composition has multiple tracks (for running parallel flows), using a "Dedicated Load server" would fail as it would not be able to run more than one track at a time. The "Dedicated Load Server" is useful if one Track has a very heavy clip.

### Targets
A Target within CloudTest points to an application, service or website that you want to test, including its location (URL) and any authentication information necessary to successfully run a test. In most cases, the target creation is automatically added through the recording technique(s) for each target. The created target can then be modified to include such information as authentication credentials.

The targets can contain addition number of of properties. The target properties can be edited with the "Target editor". All these values would be applied any time a Clip is run against this target, for example using authentication credentials for a specific target, connection options timeouts, SSL options, specific DNS options, etc.

For more info on Targets and Target Types:
https://community.akamai.com/docs/DOC-8797-targets-target-types-and-target-options

### Custom Properties
Custom Properties can be added at the Clip, Track or Band level depending on the scope we want for that value to be available. Custom properties allow capturing data values from previous messages dynamically and save them for later use on following step messages in the Clip. The typical example would be capturing a SESSIONID value from the initial requests to further use it in following messages.

Properties can also be set with an "Override value" which is a sort of initial value that can be set.

#### Global Properties List
In the "Global Properties" a list of key value pairs can be defined so it can be available on multiple compositions.

About properties:
https://community.akamai.com/docs/DOC-8901-property-management-between-parent-and-child-clips

### Seed Data
Allows importing CSV files or external data sets that can be used into custom properties. A list of values could be tied to a custom property to be used in clip in a way that each iteration would use a each value from the list.

For more info on using Seed Data:
https://community.akamai.com/docs/DOC-8894-creating-and-editing-seed-data

### Scripts
You can plug in a Javascript along with the transactions in the Clip. There's full API that allow controlling the flow of the clip.  There's a comprehensive API for CloudTest.  For example, the response code from a previous step of the Clip can be saved and used in the following step of the Clip.

Javascript can be added in the "Scripts" item. There are reference pages for the API objects and methods.

For example, to get a response code out of a clip step and add it to a custom property, the following javascript code snippet could be used:

```javascript
var msg=$context.currentItem.previousItem;

var responseCode = msg.getResponse(msg.RESPONSE_HTTP_STATUSCODE);
$context.currentClip.propertyList.setPropertyValue("ResponseCode", responseCode);
```
The best place to put the script is right after the transaction we want to get the code from.
