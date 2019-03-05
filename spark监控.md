#### Application整体监控
从yarn能监控到memory和cpu，拿到的是所有的container分配的资源\*时间的加和。
- 拿到方式
```python
url = '{rm}/ws/v1/cluster/apps/{app_id}'.format(
            rm=self.active_rm, app_id=app_id
        )
```
- 文档里有详细的解释
https://hadoop.apache.org/docs/r2.7.3/hadoop-yarn/hadoop-yarn-site/ResourceManagerRest.html
摘抄出来
    - memorySeconds  long  The amount of memory the application has allocated (megabyte-seconds)
    - vcoreSeconds  long  The amount of CPU resources the application has allocated (virtual core-seconds)

- 源码里对这两个值的注释
```java
  /**
   * Get the aggregated amount of memory (in megabytes) the application has
   * allocated times the number of seconds the application has been running.
   * @return the aggregated amount of memory seconds
   */
  @Public
  @Unstable
  public abstract long getMemorySeconds();


  /**
   * Get the aggregated number of vcores that the application has allocated
   * times the number of seconds the application has been running.
   * @return the aggregated number of vcore seconds
   */
  @Public
  @Unstable
  public abstract long getVcoreSeconds();
```
注意这是个aggregation。