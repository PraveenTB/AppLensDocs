## About this Detector

* This detector looks at the AntaresIISLogFrontEndTable and specifically at the Cs_uri_query. The detector looks for requests where this column does not contain "DWAS-Handler-Name=", which means that the DWAS handler on the worker processed the request. 
* It also looks at AntaresIISLogWorkerTable where S_reason is Connection_Abandoned_By_ReqQueue or Request_Cancelled
* When this is not present it means that for some reason the request did not make it to the worker.
* The metrics consist of Sc_status, Sc_substatus and Sc_win32_status
* You can get details on Sc_win32_status codes [here](https://msdn.microsoft.com/en-us/library/ms681381.aspx) 
* Details of S_reason codes is [here](https://support.microsoft.com/en-us/help/820729/error-logging-in-http-apis)
* Break down of request dropped categories
  * _Client Quit_: AntaresIISLogFrontEndTable Sc_win32_status=64
     * Client gone. Usually a symptom of higher time taken for request. Look at the User-Agent to see if this is some kind of pinger (which tends to have lower time limits), as opposed to a browser.
  * _Platform Issue - Transient Issue_: AntaresIISLogFrontEndTable Sc_win32_status=1236
     * Transient issue when worker is unreachable from the FE. This issue is seen in cases where requests got routed to a worker in a bad state for some time. Before our system realized that this is bad, and needs to be taken out.
  * _Platform Issue - Slow worker_: AntaresIISLogFrontEndTable Sc_win32_status=121
     * This requset took longer than 230 seconds to execute at the worker
  * _Platform Issue - Could Not Connect to Worker_ : AntaresIISLogFrontEndTable Sc_win32_status=12002
     * This is when we couldn’t connect to worker. On our end, the moment we see this error happening, we take steps to prevent further requests from getting routed to this worker.
  * _App Aborted_ : AntaresIISLogWorkerTable S_reason=Request_Cancelled 
     * Purely an App issue. App calls AbortRequest() API to cancel the request. This can also be done through an URL_Rewrite rule
  * _Platform Issue - Unknown_ : AntaresIISLogWorkerTable S_reason=Connection_Abandoned_By_ReqQueue 
     * This could be caused by various platform issues like storage volume failover
