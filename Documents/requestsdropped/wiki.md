## About this Detector

* This detector looks at the Front End IIS logs and specifically at the Cs_uri_query. The detector looks for requests where this column does not contain "DWAS-Handler-Name=", which means that the DWAS handler on the worker processed the request. 
* When this is not present it means that for some reason the request did not make it to the worker.
* The metrics consist of Sc_status, Sc_substatus and Sc_win32_status
* You can get details on Sc_win32_status codes [here](https://msdn.microsoft.com/en-us/library/ms681381.aspx) 
* Some common Sc_win32_status codes

Sc_win32_status | Code | Description
--- | --- | ---
12030 | ERROR_INTERNET_CONNECTION_ABORTED | The connection with the server has been terminated.
0 | ERROR_SUCCESS | The operation completed successfully.
64 | ERROR_NETNAME_DELETED | The specified network name is no longer available.
1236 | ERROR_CONNECTION_ABORTED | The network connection was aborted by the local system.
121 | ERROR_SEM_TIMEOUT | The semaphore timeout period has expired.
12002 | ERROR_INTERNET_TIMEOUT | The request has timed out.
