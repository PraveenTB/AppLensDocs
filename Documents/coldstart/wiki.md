## About this Detector

* This detector looks specifically at EventId 15101 which DWAS emits when a site process is starting up.
* The message for the event is "The site '%1' has taken %2 ms to warmup." 
* This detector considers any cold starts taking more then ten seconds abnormal
