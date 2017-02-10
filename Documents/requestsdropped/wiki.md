## About this Detector

* This detector looks at the Front End IIS logs and specifically at the Cs_uri_query. The detector looks for requests where this column does not contain "DWAS-Handler-Name=", which means that the DWAS handler on the worker processed the request. 
* When this is not present it means that for some reason the request did not make it to the worker.
* The metrics consist of Sc_status, Sc_substatus and Sc_win32_status
* You can get details on Sc_win32_status codes [here](https://msdn.microsoft.com/en-us/library/ms681381.aspx) 
* Some common Sc_win32_status codes
  * 12030 _ERROR INTERNET CONNECTION ABORTED_
     * W3wp terminated unexpectedly: DWAS killed w3wp because it did not terminate gracefully within 30 seconds.
     * W3wp terminated unexpectedly: App itself crashed on its own.     
     * App calls AbortRequest() API to cancel the request. This can also be done through an URL Rewrite rule
  * 64 _ERROR NETNAME DELETED_
     * Client gone. Usually a symptom of higher time taken for request. Look at the User-Agent to see if this is some kind of pinger (which tends to have lower time limits), as opposed to a browser.
  * 1236 _ERROR CONNECTION ABORTED_
     * Transient issue when worker is unreachable from the FE. I’ve seen cases where requests got routed to this type of workers for about 9-10 minutes. Before our system realized that this is bad, and needs to be taken out.
  * 121 _ERROR SEM TIMEOUT_
     * This requset took longer than 230 seconds to execute at the worker
  * 12002 _ERROR INTERNET TIMEOUT_
     * This is when we couldn’t connect to worker. On our end, the moment we see this error happening, we take steps to prevent further requests from getting routed to this worker.
  * 0 _ERROR SUCCESS_: The operation completed successfully.

