# Introduction #

How to guide for setting up a dedicated MogileFS storage server on Solaris type boxes. I've tested this on [Nexenta CP 2](http://www.nexenta.org) and it probably works on Opensolaris as well. This will only provide a storage server. You still need a tracker box somewhere. This is unsupported by the core MogileFS devs and you should probably understand how it works before you deploy it.

The main reason for running MogileFS on Solaris is to use ZFS for storing files. ZFS checksums all the data so bit-rot can be found.

# High Level Overview #

The included guide replaces mogstored with nginx for get/put support.

**Not having mogstored will make your FSCK runs incredibly slow (2-20 fids/sec)**

**As of 2.37 mogstored runs great on Nexenta CP 2 and 3**

**I recommend the updated guide [MogileFSonNexentaCP](http://code.google.com/p/mogilefs/wiki/MogileFSonNexentaCP)**

---
