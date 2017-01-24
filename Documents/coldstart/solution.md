## Possible Solutions
* A long cold start can cause requests to time out as they are waiting for the process to warm up.
* If they are only running on one instance, they can be vulnerable to downtime and high during UD walks when their site is allocated on a new worker, so they should consider scaling to two instances to avoid that.
* A cold start will happen during a deployment and it is a preferred method to deploy first to a staging slot and allow the site to warm up before it swapping with production
