## About this Detector

* This detector looks at the AntaresIISLogFrontEndTable and specifically at the Cs_uri_query. The detector looks for requests where this column does not contain "DWAS-Handler-Name=", which means that the DWAS handler on the worker processed the request. 
* It also looks at AntaresIISLogWorkerTable where S_reason is Connection_Abandoned_By_ReqQueue or Request_Cancelled
* When this is not present it means that for some reason the request did not make it to the worker.
* The metrics consist of Sc_status, Sc_substatus and Sc_win32_status
* You can get details on Sc_win32_status codes [here](https://msdn.microsoft.com/en-us/library/ms681381.aspx) 
* Details of S_reason codes is [here](https://support.microsoft.com/en-us/help/820729/error-logging-in-http-apis)
* Break down of request dropped categories
  * _Transient Issue_: AntaresIISLogFrontEndTable Sc_win32_status=1236,121,12002
     * Transient issue when worker is unreachable from the FE. This issue is seen in cases where requests got routed to a worker in a bad state for some time. Before our system realized that this is bad, and needs to be taken out.
  * _App Aborted_ : AntaresIISLogWorkerTable S_reason=Request_Cancelled 
     * Purely an App issue. App calls AbortRequest() API to cancel the request. This can also be done through an URL_Rewrite rule
  * _Connection Abandoned By Request Queue_ : AntaresIISLogWorkerTable S_reason=Connection_Abandoned_By_ReqQueue 
     * The request que is abadoning requests as the worker(s) may not have resources(memory, CPU, threads, ports, etc..) to handle them. This is most likely due to an app isue causing a leak
