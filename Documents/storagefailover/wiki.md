## About this Detector

* File Server Failover: 
Occurs when planned upgrades or unplanned downtimes and any other disruptions with Azure Storage that occur on servers that serve the content share. During this transition is is possible the content share will be in read-only for a short time (a couple minutes). This could surface as errors in apps that write to the content share and do not have error handling in place to catch / retry write operation failures.

* Latency Failover: 
This occurs when the server hosting the read/write content share becomes unavailable, the App is restarted to use a read-only replica until the read/write volume is available and responsive again.

* Local Cache Event: 
This event occurs when the App is restarted to use the content on the local instance once it has completed copying it from the content share. This activity occurs when the Local Cache App settings were changed (enable only shown or any Local Cache setting change surfaced?), the App is stopped and started or the App is starting on a new instance. 
Note: The Local Cache failover is not flagged during a Downtime period. 

Local Cache details
https://docs.microsoft.com/en-us/azure/app-service/app-service-local-cache
