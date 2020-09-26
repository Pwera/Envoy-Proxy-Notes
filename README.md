# Envoy Proxy Notes

# Envoy Architecture:
- Downstream/Upstream
![Downstream/Upstream](/img/envoy0.png)
  * Anything in front of Envoy is Downstream
  * Anything in back of Envoy is Upstream
  * Communication between Downstream & Upstream is done through 'Side Car'
  * Requests come from Downstream
  * Responses come from Upstream
- Clusters
![Clusters](/img/envoy1.png)
  * Group of hosts/endpoints are called a cluster
  * Cluster has a load balancing policy
- Listeners
  * Listen on a port for downstream clinets
  * Similar to Frontend in HAProxy
  * Network Filters are applied to Listeners (mapping to a cluster)
    * TCP/HTTP Filters
    * Transport Sockets TLS
- Threading Model
  * Single process multi-threaded model
  * Each thread is bound to a single connection
  * No coordination between threads
- Connection Pools
![Connection Pools](/img/envoy2.png)
  * Each host in a cluster gets 1 or more connection pools
  * Each protocol get a pool HTTP 1.1, HTTP/2
  * More pools allocated per Priority or socket options ( There are default and high priority pools)
  * Connection Pools are per worker thread
- Network Filters
  * How Envoy maps Listeners and Clusters
  * TCP Proxy Network Filter
    *  envoy.filters.network.tcp_proxy
  * HTTP Proxy Network Filter
    * envoy.filters.network.http_connection_manager
  * MongoDB/MySQL Network Filter
