## Possible Solutions
* If problem is only on one instance, try restarting the worker process on that instance
* Scale up to a larger instance size
* Run DaaS to diagnose the problem in your application
* If the memory is consistently high across instance(s), then you may want to break the Web Apps across multiple App Service Plans
* If there is a temporary spike in memory, then you may want to check if the application has any resource intesive activtity that could trigger the memory spike

