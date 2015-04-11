The following is a high-level overview of how MogileFS works, and what all the moving pieces are.

# The involved parties are #

  * **Application**: thing that wants to store/load files
  * **Tracker** (the mogilefsd process): event-based parent process/message bus that manages all client communication from applications (requesting operations to be performed), including load balancing those requests onto "query workers", and handles all communication between mogilefsd child processes. You should run 2 trackers on different hosts, for HA, or more for load balancing (should you need more than 2). The child processes under mogilefsd include:
    * Replication -- replicating files around
    * Deletion -- deletes from the namespace are immediate; deletes from filesystems are async
    * Query -- answering requests from clients
    * Reaper -- reenqueuing files for replication after a disk fails
    * Monitor -- monitor health and status of hosts and devices
    * ...
  * **Database** -- the database that stores the MogileFS metadata (the namespace, and which files are where). This should be setup in a HA config so you don't have a single point of failure.
  * **Storage** **Nodes** -- where files are stored. The storage nodes are just HTTP servers that do DELETE, PUT, etc. Any WebDAV server is fine, but mogstored is recommended. mogilefsd can be configured to use two servers on different ports... mogstored for all DAV operations (and sideband monitoring), and your fast/light HTTP server of choice for GET operations. Typically people have one fat SATA disk per mountpoint, each mounted at /var/mogdata/devNN.

High-level flow:

  * app requests to open a file (does RPC via library to a tracker, finding whichever one is up). does a "create\_open" request.
  * tracker makes some load balancing decisions about where it could go, and gives app a few possible locations
  * app writes to one of the locations (if it fails writing to one midway, it can retry and write elsewhere).
  * app (client) tells tracker where it wrote to in the "create\_close" API.
  * tracker then links that name into the domain's namespace (via the database)
  * tracker, in the background, starts replicating that file around until it's in compliance with that file class's replication policy
  * later, app issues a "get\_paths" request for that domain+key (key == "filename"), and tracker replies (after consulting database/memcache/etc), all the URLs that the file is available at, weighted based on I/O utilization at each location.
  * app then tries the URLs in order. (although the tracker's continually monitoring all hosts/devices, so won't return dead stuff, and by default will double-check the existence of the 1st item in the returned list, unless you ask it not to...)