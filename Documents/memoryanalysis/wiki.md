## About this Detector

This detector looks at memory on each worker. There are five time series returned by this detector: 
* "Percent Memory Used": percent of memory used by all processes on the worker based on total available memory on the worker
* "Memory Usage - Total": Total Memory used on the worker in MB
* "Memory Usage - App Pools": Total memory used by all app pools
* "Memory Usage - Services": Total Memory used by antares services
* "Memory Usage - Other": Total Memory used by processes that do not fall into one of the above categories
