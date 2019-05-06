# hbaseexample

HBase Cell TTL
Changes: https://issues.apache.org/jira/browse/HBASE-10560

HBase Put Code Analysis
https://blog.csdn.net/bryce123phy/article/details/51279878

https://www.jianshu.com/p/37570a5e2f95

# hbase config
hbase.hregion.memstore.mslab.enabled
hbase.hregion.memstore.mslab.chunksize
hbase.hregion.memstore.mslab.max.allocation
should be set an appropriate value. If the cell size varies, we should use different table spaces. Especially with G1 GC users have reported that you can turn MSLABs off, without incurring any measurable penalty.

# hbase block cache
* root index
  * block index
  * bloom filter
* data block

# java socket
* SO_LINGER -> false, whtaever(default)
  * immediately return from close but OS is waiting to handshake complete. time_wait could happen in this case
* SO_LINGER -> true, 0
  * immediately return from close, the socket is closed forcefully, with a TCP RST 
* SO_LINGER -> true, x 
  * a close() will block pending the transmission and acknowledgement of all data written to the peer, at which point the socket is closed gracefully. Upon reaching the linger timeout, the socket is closed forcefully, with a TCP RST.
  
# Why needs Bloom Filter
For example, the LSM-tree algorithm can be slow when looking up keys that do not exist in the database: you have to check the memtable, then the segments all the way back to the oldest (possibly having to read from disk for each one) before you can be sure that the key does not exist. In order to optimize this kind of access, storage engines often use additional Bloom filters [15]. (A Bloom filter is a memory-efficient data structure for approximating the contents of a set. It can tell you if a key does not appear in the database, and thus saves many unnecessary disk reads for nonexistent keys.)



