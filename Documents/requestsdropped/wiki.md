## About this Detector

* This detector looks at the Front End IIS logs and specifically at the Cs_uri_query. The detector looks for requests where this column does not contain "DWAS-Handler-Name=", which means that the DWAS handler on the worker processed the request. 
* When this is not present it means that for some reason the request did not make it to the worker.
* The metrics consist of Sc_status and Sc_win32_status
* You can get details on Sc_win32_status codes here: https://msdn.microsoft.com/en-us/library/ms681381.aspx 
