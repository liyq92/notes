1. 缓存连接

在 MySQL Router 中，可以使用缓存连接来避免频繁的创建连接和断开连接。缓存连接可以提高性能，降低资源消耗。

可以通过以下设置来启用缓存连接：

```
[DEFAULT]
bind_address=192.168.1.100

[router]
cached_connections=100
```

这里，cached_connections 设置为 100 表示 Router 最多缓存 100 个连接。

2. 负载均衡算法

MySQL Router 支持多种负载均衡算法，包括最近最少使用（Least Recently Used，LRU）、加权轮询（Weighted Round Robin，WRR）、随机（Random）、最短连接数（Least Connections，LC）等。

可以根据实际情况选择合适的负载均衡算法，如需要让某个节点承担更多的请求，可以选择加权轮询算法，将该节点的权重调高。

可以通过以下设置来选择负载均衡算法：

```
[DEFAULT]
bind_address=192.168.1.100

[router]
routing_strategy=WeightedRoundRobin
```

这里，routing_strategy 设置为 WeightedRoundRobin，表示使用加权轮询算法。

3. 缓存元数据

MySQL Router 可以缓存元数据（metadata）来提高性能，例如数据库和表的结构信息，以及用户和权限信息。

可以通过以下设置来启用元数据缓存：

```
[DEFAULT]
bind_address=192.168.1.100

[router]
metadata_cache_size=10000
```

这里，metadata_cache_size 设置为 10000，表示缓存 10000 条元数据信息。

4. 使用 SSL

如果需要保证数据传输的安全性，可以启用 SSL。

可以通过以下设置来启用 SSL：

```
[DEFAULT]
bind_address=192.168.1.100

[router]
ssl_mode=REQUIRED
ssl_ca=/path/to/ca.pem
ssl_cert=/path/to/client-cert.pem
ssl_key=/path/to/client-key.pem
```

这里，ssl_mode 设置为 REQUIRED，表示强制启用 SSL。ssl_ca、ssl_cert、ssl_key 分别指定 CA、客户端证书和客户端私钥的路径。

5. 长连接

使用长连接可以避免频繁的建立和断开连接，以提高性能。

可以通过以下设置来启用长连接：

```
[DEFAULT]
bind_address=192.168.1.100

[router]
use_persistent_connections=True
```

这里，use_persistent_connections 设置为 True，表示启用长连接。

6. 日志级别

日志级别可以影响性能和日志大小，建议根据实际情况选择合适的日志级别。

可以通过以下设置来设置日志级别：

```
[DEFAULT]
bind_address=192.168.1.100

[router]
log_level=DEBUG
```

这里，log_level 设置为 DEBUG，表示设置日志级别为调试级别。

7. 合理配置缓存大小

对于频繁查询、连接较多的应用，可以将缓存大小适当调大，以提高数据库连接性能。但如果过大，反而可能导致缓存失效，造成内存压力。

可以通过以下设置来设置缓存大小：

```
[DEFAULT]
bind_address=192.168.1.100

[router]
cache_size=10000
```

这里，cache_size 设置为 10000，表示设置缓存大小为 10000。

8. 避免连接池过多

一些应用程序由于不恰当的设计可能导致打开许多连接而没有及时释放，Connection pool 过多，可以适当减少 Connection Pool 的大小，但是要避免 Connection Pool 过小，造成 Connection 的频繁创建和释放。可以根据数据库的请求量和资源整体状况等因素适当调整连接池大小。

总体上，要想让 MySQL Router 的性能更好，需要对其进行合理的配置和优化。以上优化方式仅供参考，实践中还需对具体环境和需求进行调整。