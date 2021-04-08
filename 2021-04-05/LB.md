## 简述常见的负载均衡算法
负载均衡算法用于确定流量应该被分发到哪一个健康的服务器上，常见的几个算法如下：
### 1. 轮询（Round Robin）
- 调度器通过"轮询"调度算法将外部请求按顺序轮流分配到集群中的真实服务器上,它均等地对待每一台服务器,而不管服务器上实际的连接数和系统负载｡
- 举例：负载均衡器会将第一个请求分配给第一个服务器，然后下一个请求分配给第二个服务器，这样分配下去分配完一轮之后回到开头分配给第一个服务器（操作系统调度算法复习一下）。
- 应用场景：这种方式比较适合各服务器处理能力相同而且每个业务处理量差不多的时候。

### 2. 最少连接（Least Connections）
- 调度器通过"最少连接"调度算法动态地将网络请求调度到已建立的链接数最少的服务器上｡
- 如果集群系统的真实服务器具有相近的系统性能,采用"最小连接"调度算法可以较好地均衡负载｡
- 负载均衡器会选择当前连接最少的服务器。

### 3. IP hash — 源地址散列调度(SourceHashingScheduling)
- 在这个算法下，负载均衡器根据请求源的IP来决定分发给哪个服务器。
- "源地址散列"调度算法根据请求的源IP地址,作为散列键(HashKey)从静态分配的散列表找出对应的服务器,若该服务器是可用的且未超载,将请求发送到该服务器,否则返回空｡
- 这个方法保证了一个特定的用户会一直访问相同的服务器。


---

其他还有一些不算太常见的算法，比如Url hash、Random，以及下面的几个：

#### 4.加权轮询调度(WeightedRound-RobinScheduling)

调度器通过"加权轮询"调度算法根据真实服务器的不同处理能力来调度访问请求｡这样可以保证处理能力强的服务器处理更多的访问流量｡调度器可以自动问询真实服务器的负载情况,并动态地调整其权值｡

#### 5.加权最小连接调度(WeightedLeast-ConnectionScheduling)

在集群系统中的服务器性能差异较大的情况下,调度器采用"加权最少链接"调度算法优化负载均衡性能,具有较高权值的服务器将承受较大比例的活动连接负载｡调度器可以自动问询真实服务器的负载情况,并动态地调整其权值

#### 6.基于局部性的最少链接(Locality-BasedLeastConnectionsScheduling)

基于局部性的最少链接"调度算法是针对目标IP地址的负载均衡,目前主要用于Cache集群系统｡该算法根据请求的目标IP地址找出该目标IP地址最近使用的服务器,若该服务器是可用的且没有超载,将请求发送到该服务器;若服务器不存在,或者该服务器超载且有服务器处于一半的工作负载,则用"最少链接"的原则选出一个可用的服务器,将请求发送到该服务器｡

#### 7. 带复制的基于局部性最少链接(Locality-BasedLeastConnectionswithReplicationScheduling)

- Cache集群系统 ：带复制的基于局部性最少链接"调度算法也是针对目标IP地址的负载均衡,目前主要用于Cache集群系统｡它与LBLC算法的不同之处是它要维护从一个目标IP地址到一组服务器的映射,而LBLC算法维护从一个目标IP地址到一台服务器的映射｡
- 该算法根据请求的目标IP地址找出该目标IP地址对应的服务器组,按"最小连接"原则从服务器组中选出一台服务器,若服务器没有超载,将请求发送到该服务器,若服务器超载;则按"最小连接"原则从这个集群中选出一台服务器,将该服务器加入到服务器组中,将请求发送到该服务器｡同时,当该服务器组有一段时间没有被修改,将最忙的服务器从服务器组中删除,以降低复制的程度

#### 8.目标地址散列调度(DestinationHashingScheduling)

目标地址散列"调度算法根据请求的目标IP地址,作为散列键(HashKey)从静态分配的散列表找出对应的服务器,若该服务器是可用的且未超载,将请求发送到该服务器,否则返回空