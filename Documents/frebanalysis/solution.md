## Possible Solutions

* Check your application events in Application events in Azure Portal
* To diagnose errors in your application code, Enable Application Insights.
* [Learn How to enable Application Insights](https://azure.microsoft.com/en-us/documentation/articles/app-insights-overview "Application Insights - introduction")
* If you troubleshoot node.js application please refer to this [Troubleshoot Guide](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-nodejs-best-practices-and-troubleshoot-guide) 
* If your application uses OWIN - consider to use Microsoft.Owin.Diagnostics package. It contains middleware that catches unhandled exceptions and displays an HTML page with error details or you can enable katana [Logs](http://katanaproject.codeplex.com/wikipage?title=Debugging&referringTitle=Documentation)
