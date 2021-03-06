## 其他面试题

> 不太好分类的面试题，有几个准备测开和技术运维时候找的题（这个和开发问的问题大同小异，只有个别针对性较强的问题，毕竟也是开发），还有数据量很大时的编程题。


## 测开

### 1. hash冲突：
**hash表**：【正向快速、逆向困难、输入敏感、冲突避免】
**hash冲突**：两个不同的对象计算的hash值相同，就出现了冲突。
**怎么解决：**
- 开放定址法【再散列法】：发生冲突后按照某一次序找到下一个空闲的地址。
	-  线性再散列：di = 1, 2, 3… 从发生冲突的下一个单元开始依次探查是否有空闲，若到表尾还没游空闲就从表头开始接着探查；
	-  二次再散列：di = 1^2，-1^2，2^2，-2^2…. 在表的左右进行跳跃式探测，比较灵活；
	-  随机再散列：di = 伪随机序列。
- 再哈希法：同时构造多个hash函数，一个不行换下一个。不易产生聚集，但增加了计算时间；
- 链地址法：将所有hash值相同的元素存放在一个链表中，并将链表头节点放入哈希表对应地址。插入删除时访问链表，适用于经常插入删除的情况；
- 建立公共溢出区：建立基本表和溢出表，和基本表发生冲突的都存进溢出表。



### 2. 接口
- python接口类：只是定义了一些方法，而没有去实现，多用于程序设计时，只是设计需要有什么样的功能，但是并没有实现任何功能，这些功能需要被另一个类（B）继承后，由 类B去实现其中的某个功能或全部功能。在python中接口由抽象类和抽象方法去实现，接口是不能被实例化的，只能被别的类继承去实现相应的功能。
- 软件接口：负责在不同的系统间，或者同意系统内不同模块之间传输或接收数据的并做处理的类或者函数。


### 3. 软件测试四个阶段：

	1. 单元测试：检验软件最小单元的正确性，消除局部模块上的逻辑或功能的错误和缺陷。
		a. 阶段：编码后；
		b. 对象：最小单元——模块；
		c. 人员：测试人员，开发人员；
		d. 依据：代码和注释 + 详细设计文档；
		e. 方法：白盒测试；
		f. 内容：模块接口测试，局部数据结构测试，路径测试，错误处理测试，边界测试。
	2. 集成测试：将程序模块使用适当的集成策略组装起来，对系统的接口及继承后的功能进行正确性检测。主要检测软件单位之间的接口是否正确。
		a. 阶段：单元测试后；
		b. 对象：模块间的接口；
		c. 人员：测试人员，开发人员；
		d. 依据：单元测试的模块 + 概要设计文档；
		e. 方法：黑盒 + 白盒；
		f. 内容：模块之间的数据传输、模块间的功能冲突、模块组装功能正确性、全局数据结构、单模块缺陷对系统的影响。
	3. 系统测试：对功能、性能及软件所运行的软硬件环境进行测试，包括回归测试和冒烟测试。
		a. 阶段：集成测试后；
		b. 对象：整个系统；
		c. 人员：黑盒测试人员；
		d. 依据：需求规格说明文档；
		e. 方法：黑盒测试；
		f. 内容：功能、界面、可靠性、易用性、性能、兼容性、安全性等。
	4. 验收测试：确保软件准备就绪，按照项目合同、任务书、双方约定的验收依据文档，向软件购买者展示该软件系统满足需求。
		a. 阶段：系统测试后；
		b. 对象：整个系统；
		c. 人员：用户或需求方；
		d. 依据：用户需求、验收标准；
		e. 方法：黑盒测试；
		f. 内容：同系统测试。



### 4. 测试方法分类
- 白盒测试：关注内部处理逻辑和输入输出；分为静态测试（不运行，模拟分析）和动态测试（运行实际用例），动态测试主要技术有路径和分支测试；
- 黑盒测试：不关注内部逻辑，只关注输入输出。是更接近用户的测试方法，会关注易用性、性能、用户界面、业务流程等内容。
- 灰盒测试：集成测试阶段同时使用白盒测试和黑盒测试即为灰盒测试。是介于白盒测试与黑盒测试之间的一种测试，灰盒测试多用于集成测试阶段，不仅关注输出、输入的正确性，同时也关注程序内部的情况。灰盒测试不像白盒那样详细、完整，但又比黑盒测试更关注程序的内部逻辑，常常是通过一些表征性的现象、事件、标志来判断内部的运行状态。



## 技术运维


### 1. CDN加速
**CDN：内容分发网络**  
通过在现有的网络中中增加一层新的CACHE(缓存)层，将网站的内容发布到最接近用户的网络”边缘“的节点，使用户可以就近取得所需的内容，提高用户访问网站的响应速度。

**解析过程：**
浏览器向域名解析服务器发出解析请求，由于CDN 对域名解析过程进行了调整，所以用户端一般得到的是该域名对应的 CNAME 记录（存有CDN节点），此时浏览器需要再次对获得的 CNAME 域名进行解析才能得到缓存服务器实际的IP 地址。 注：在此过程中，DNS 解析服务器根据用户端的源IP 地址，如地理位置(北京还是上海)、接入网类型(电信还是网通)将用户的访问请求定位到离用户路由最短、位置最近、负载最轻的Cache 节点(缓存服务器)上，实现就近定位。定位优先原则可按位置、可按路由、也可按负载等。


### 2. 分布式
- **Hadoop**是由java语言编写的，在分布式服务器集群上存储海量数据并运行分布式分析应用的开源框架。Hadoop的框架最核心的设计就是：HDFS和MapReduce。HDFS为海量的数据提供了存储，则MapReduce为海量的数据提供了计算。
- **HDFS**是一个分布式文件系统：引入存放文件元数据信息的服务器Namenode和实际存放数据的服务器Datanode，对数据进行分布式储存和读取。把HDFS理解为一个分布式的，有冗余备份的，可以动态扩展的用来存储大规模数据的大硬盘。
- **MapReduce**是一个计算框架：MapReduce的核心思想是把计算任务分配给集群内的服务器里执行。通过对计算任务的拆分（Map计算/Reduce计算）再根据任务调度器（JobTracker）对任务进行分布式计算。把MapReduce理解成为一个计算引擎，按照MapReduce的规则编写Map计算/Reduce计算的程序，可以完成计算任务。


### 3. DevOps
是开发（Development）和运维（Operations）的组合，旨在促进开发和运维人员之间的沟通，使软件的开发、测试和发布更快捷并且可靠。实际上这个名字忽略了测试，DevOps其实是一个闭环，从规划、开发，到测试、部署、运维都涵盖在里面。我理解的DevOps是一种思想，一种方案。


### 4. 机房建设的考虑
	1. 安全：包括用电安全和制冷
	2. 能源：需要稳定供电保证运行
	3. 可扩展性：升级扩展的时候比较方便，能向下兼容
	4. 维护方便


### 5. 服务运行时监控什么：
	1. CPU利用率
	2. 资源的使用情况
	3. 告警情况（告警数、告警类别）
	4. 网络速率
	5. 存储空间使用情况


## 编程题

### 1. 10亿个数字中最大的100个：
- **使用最小堆**：先取出100个元素建立最小堆（插入法heappush建堆时间复杂度为O(klogk)，下拉交换法heapify建堆时间复杂度为O(k)），然后依次用剩下的元素和堆顶比较，若新元素更小则丢弃，否则将其插入堆中并维护堆性质。总的时间复杂度为O(klogk + (n-k)logk) = **O(nlogk)**，空间复杂度**O(n)**。
- **优化**：将原文件分割成多个子文件，找出每个子文件中最大的100个数，再使用结果集进行归并获得总的最大的100个数。


### 2. 1亿数据如何排序：
- 分成几块，每块分别使用堆排序，然后将最后结果归并；
- 为什么不用快速排序，因为堆排序能保证一定是O(nlogn)，而快速排序在较差情况可能为O(n^2)；


### 3. 排序算法的选择：
- 当n较大时，选用时间复杂度为O(nlogn)的排序算法：
	- 要求稳定性时使用归并排序，可以在子序列较小时使用插入排序提高效率；
	- 数据随机分布且有足够辅助内存时使用快速排序；
	- 当内存有限时使用堆排序，且堆排序不会出现快速排序可能出现的最坏情况；
- 当n较小时，选用插入排序或选择排序：
- 当数据基本有序时使用插入排序或冒泡排序。


### 4. 如何判断一个数是否在40亿个整数中：
**bitmap**：使用位来表示状态。  
32位int的范围，总共就是2的32次方，大概42亿多点。可以申请2的32次方个位，每个位的0/1代表相应整数是否存在，如（11011代表数字2不存在）。一个32位整数占4个字节，2的32次方个位是2的29次方个字节，1GB约10亿个字节，共512MB内存。原来32位的整数转化成了1位的布尔值，占用空间减少了32倍。


### 5. 1亿个正整数范围是0-42亿，求出现次数是2的数字：
为每个数字分配2个位，表示其出现的次数：00表示0次，01表示1次，10表示2次，11表示大于2次。顺序扫描数组并记录出现次数，最后再扫描一遍数组找出出现两次的数字。



## 其它

### 1. Git命令：
	新建：git init
	克隆：git clone

	添加更改：git add <filename>
	添加全部更改：git add .
	删除：git rm <filename>

	提交更改：git commit -m 'commit message'
	将更改推到远程：git push origin master
	本地连接远程：git remote add origin <server>
	本地与远程同步：git pull

	新建分支：git checkout -b <branch>
	切换到master分支：git checkout master
	删除分支：git branch -d <branch>
	将分支推到远程：git push origin <branch>

	将更改合并到另一分支：git merge <branch>
	比较两分支：git diff <source> <target>

	新建标签：git tag <tag> <commit id>
	提交id:  git log

	复原：git checkout --<filename>


### 2. 中间件
将具体业务和底层逻辑解耦的组件，使用服务的人不需要知道底层逻辑的实现原理。

中间件能给客户带来什么：系统开发更简单，基于成熟的组件来做，可以极大的减少技术选择成本。在系统交互的时候，直接使用中间件进行连接和交互，以及代码开发和人工成本。


### 3. 内存对齐：
由于计算机不是以字节为单位访问数据，而是以块（2，4，6，8字节）为单位。如果不进行内存对齐，原本一次完成的读写可能需要多次，还有额外的数据merge或数据分离操作，这些使得效率低下。


### 4. 常见加密算法：
- 对称加密：加密和解密使用同样的密钥，用同一种方式安全地共享密钥很难。如AES。
- 非对称加密：加密和解密使用不同的密钥（公共密钥/私有密钥）。如RSA。
- 数字证书：属于非对称加密。一个组织可以使用证书将一组公钥和私钥与其拥有者相关联。


### 5. 哈希算法：
- 哈希算法主要用于保障数据的真实性（即完整性），发送方将数据和哈希值一同发送，接收方通过相同的哈希函数计算哈希值来验证数据在通信过程中是否被篡改。【正向快速、逆向困难、输入敏感、冲突避免】
- MD5：消息填充，最后的消息长度是512的整数倍，生成128位报文摘要；
- SHA：
	- SHA1对明文的预处理和MD5相同，得到512整数倍的消息。区别在于消息不得长于2^64次方，并生成160位的报文摘要。
	- SHA256产生256位的报文摘要。


### 6. 设计模式：
是一套被大家广泛认可和使用的，经过分类的代码设计经验的总结。

**工厂模式**：使一个类的实例化延迟到子类。
定义一个用于创建对象的接口，让子类决定实例化哪一类。

**单例模式**：保证系统中一个类只有一个对象的实例。
- 为什么使用单例模式：
	• 单例模式节省公共资源；
	• 单例模式方便控制。
- 实现：
	• 构造私有：为了防止一个类被多次实例化，将类的构造函数设为私有；
	• 以静态方法返回实例：提供类的方法让外界获取实例对象；
	• 只实例化一次，之后都使用实例化后的对象。
- 两种模式：
	• 饿汉模式：先创建好实例，需要时直接使用。容易造成资源浪费（一直不使用）；
	• 懒汉模式：需要使用的时候再构造实例，解决了资源浪费。但是在并发时可能同时实例化多个对象，需要用锁控制。
