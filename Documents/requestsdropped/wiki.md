## About this Detector

* This detector looks at the Front End IIS logs and specifically at the Cs_uri_query. The detector looks for requests where this column does not contain "DWAS-Handler-Name=", which means that the DWAS handler on the worker processed the request. 
* When this is not present it means that for some reason the request did not make it to the worker.
* The metrics consist of Sc_status, Sc_substatus and Sc_win32_status
* You can get details on Sc_win32_status codes [here](https://msdn.microsoft.com/en-us/library/ms681381.aspx) 
* Some common Sc_win32_status codes
  * 12030 **ERROR INTERNET CONNECTION ABORTED**: The connection with the server has been terminated
  * 0 **ERROR SUCCESS**: The operation completed successfully.
  * 64 **ERROR NETNAME DELETED**: The specified network name is no longer available.
  * 1236 **ERROR CONNECTION ABORTED**: The network connection was aborted by the local system.
  * 121 **ERROR SEM TIMEOUT**: The semaphore timeout period has expired.
  * 12002 **ERROR INTERNET TIMEOUT**: The request has timed out.

