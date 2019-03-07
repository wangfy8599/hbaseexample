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



