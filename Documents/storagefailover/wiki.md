## About this Detector

* File Server Failover: 
Occurs when planned upgrades or unplanned downtimes and any other disruptions with Azure Storage that occur on servers that serve the content share.

* Latency Failover: 
This occurs when the server hosting the read/write content share becomes unavailable, the App is restarted to use a read-only replica until the read/write volume is available and responsive again.

* Local Cache Event: 
This event occurs when the App is restarted to use the content on the local instance once it has completed copying it from the content share. This activity occurs when the Local Cache App settings were changed (enable only shown or any Local Cache setting change surfaced?), the App is stopped and started or the App is starting on a new instance. 

Local Cache details
https://docs.microsoft.com/en-us/azure/app-service/app-service-local-cache

Original content: These problems occur possible due to latency failover, or due to file server failover. In latency failover there is no write access but there is read access. (Need details on the following as this should not occur. write there is a chance it will fail, but reads should always work in a normal service update / volume move) fileserver failover there is a momentary loss of both read and write functionality.
