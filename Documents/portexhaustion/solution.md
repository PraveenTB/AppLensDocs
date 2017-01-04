## Possible Solutions
* If problem is only on one instance, try restarting the worker process on that instance
* Scale up to a larger instance size
* If ports are consistantly getting exhausted accross instance(s), then you may want to break the Web Apps across multiple App Service Plans
* If there is a temporary spike in port exhaustion, then you may want to check if the application has any port resource intesive activtity that could trigger the spike
