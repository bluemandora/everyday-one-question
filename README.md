# everyday-one-question
made，每日一问答答案好难找，快帮我找啊！

第一周第一题：select和epoll各是什么鬼？

	就是两种IO多路复用机制啦！参考：https://segmentfault.com/a/1190000003063859（TODO：写详细一点）
	
第一周第二问：tcp断开连接有几次握手？每次是哪边发到哪边？

	4次啦！
	方向是→ ← ← →（右左左右）。（TODO：解释一下为什么）
	
第一周第三问：有哪些进程间通信方式？

	管道( pipe )：管道是一种半双工的通信方式，数据只能单向流动，而且只能在具有亲缘关系的进程间使用。进程的亲缘关系通常是指父子进程关系。
	有名管道 (named pipe) ： 有名管道也是半双工的通信方式，但是它允许无亲缘关系进程间的通信。
	信号量( semophore ) ： 信号量是一个计数器，可以用来控制多个进程对共享资源的访问。它常作为一种锁机制，防止某进程正在访问共享资源时，其他进程也访问该资源。因此，主要作为进程间以及同一进程内不同线程之间的同步手段。
	消息队列( message queue ) ： 消息队列是由消息的链表，存放在内核中并由消息队列标识符标识。消息队列克服了信号传递信息少、管道只能承载无格式字节流以及缓冲区大小受限等缺点。
	信号 ( sinal ) ： 信号是一种比较复杂的通信方式，用于通知接收进程某个事件已经发生。
	共享内存( shared memory ) ：共享内存就是映射一段能被其他进程所访问的内存，这段共享内存由一个进程创建，但多个进程都可以访问。共享内存是最快的 IPC 方式，它是针对其他进程间通信方式运行效率低而专门设计的。它往往与其他通信机制，如信号两，配合使用，来实现进程间的同步和通信。
	套接字( socket ) ： 套接字也是一种进程间通信机制，与其他通信机制不同的是，它可用于不同机器间的进程通信。


第一周第四问：jvm垃圾回收机制是怎样的？

	jvm的垃圾回收方法大体分为两种:引用计数法(存在循环引用缺陷)和根搜索算法(有延迟性，是目前的主流算法)。
	引用计数法:当一个对象被引用时，该对象的计数+1，当对象的生存周期结束时计数-1。计数为0时会调用GC进行会搜。
	根搜索算法:从GC root开始对可达的对象进行标记，然后将不可达对象从堆中清除。
	
	jvm采用分代回收的方式进行垃圾回收，
	在java堆中，新生代主要存放很快就会被GC回收或者比较小的对象，新生代的垃圾回收采用复制算法，即将新生代分为三个区Eden区和两个survivor区，默认大小为8:1:1，默认情况下会留一个survivorB不使用，在发生GC时将Eden区和使用的survivorA的存活对象放入未使用的survivorB当中去，然后对Eden和survivorA进行清理。若survivorB的大小不足以存放所有存活对象，则将存活对象暂时存放到老年代的空间当中。
	老年代主要存放对象是在新生代经历了多次回收依然存活或者特别大的对象，发生在老年代的垃圾回收采用标记-清除算法(会产生大量内存碎片)或者标记-整理算法(会造成高额的时间开销)，标记-清除算法是先老年代中存活的对象进行标记，然后将未标记的对象直接清除。标记-整理算法在标记部分与标记-清除算法一样，然后将已标记的对象向内存的一端移动，然后直接清理端边界以外的内存。
	（参考书目:《深入理解Java虚拟机》周志明）
	
第一周第5问：tcp建立连接的三次握手发的东西具体包含什么？

	第一次： SYN seq=x
	第二次： SYN seq=y ACK=x+1
	第三次： ACK=y+1

第6问：http、https从输入网址到显示网页，分别要经历哪些时间段？

第7问：魔兽争霸3读图耗时主要与哪个硬件参数有关？

第2周第1问：多个wifi并存时它们是如何处理冲突的？

	设置在不同的信道和频率

第2周第2问：简要说明对称密钥和非对称密钥的特点，为什么需要用它们。

	对称加密算法在加密和解密时使用的是同一个秘钥；而非对称加密算法需要两个密钥来进行加密和解密。对称加密算法非常容易根据原文和密文对照，在线性时间内破解。而非对称加密算法（典型的如RSA）很难被破解，这样就有效增强信息安全性，主要用于Web上避免被监听以及MITM攻击。

第2周第3问：用程序解决数独问题需要用什么方法？

	DFS

第2周第4问：写多线程程序为什么需要加锁，锁有哪些种类？

	有效处理资源分配和冲突的问题。
	互斥锁，递归锁，读写锁，旋转锁，文件锁，信号量。

第2周第5问：什么是同步、异步、阻塞、非阻塞？

	同步：发出一个调用时，没有得到结果调用就不会返回。相当于串行执行一连串任务。
	异步：发出一个调用后，继续执行后面的命令，在实际处理者得到结果之后再通知回调返回结果并处理后续相关的东西。相当于并行执行/等待若干上下文无关任务。
	阻塞：一个调用/资源请求未完成的时候进入等待状态，请求得到结果之后才能做别的事情。
	非阻塞：一个调用/资源请求未完成的时候先做别的事情，等结果来了再回到相关任务做后续处理。

第2周第6问：什么是一致性哈希？

	一种分布式哈希，特性是在移除/添加一个节点（机器，ip）时，它能够尽可能小的改变已存在 key 映射关系，尽可能的满足单调性（）的要求。

第2周第7问：面向对象三要素是什么？c++的虚态是什么，还有什么面向对象的东西？java的接口和虚函数是什么？

	封装，继承，堕胎（大雾）。C++虚态就是通过vtable进行运行时的对象确定和调用绑定。
	JAVA我不会，请补充。

第3周第1问：内存装不下所有数据时，用什么排序方法比较好？

	归并排序

第3周第2问：手写二叉树翻转算法。

第3周第3问：什么是SQL注入？如何预防？你常用的防SQL注入模块的具体内部实现？

	SQL注入，就是通过把SQL命令插入到Web表单提交或输入域名或页面请求的查询字符串，最终达到欺骗服务器执行恶意的SQL命令。最简单的比如 x' and 1=1; DROP TABLE。一般通过使用参数化调用的API或者进行输入过滤非法字符来预防。