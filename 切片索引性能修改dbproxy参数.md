> 詹溧
> 1. dbproxy的分片键要加索引；
> 2. dbproxy的线程池、内存配置要修改；
> 3. 如果缓存性能不行，也会大大影响效率 ;

测试环境：
修改dbproxy参数
![](/assets/QQ截图20160930083521.png)
![](/assets/QQ截图20160930083534.png)
![](/assets/QQ截图20160930083550.png)
这些参数之前都是默认值

* Processors                系统可用线程数，通常设为逻辑cpu的个数 
* processorExecutor         线程池大小 Processors\*8

#### 根据分片键cust\_id查询数据的效率

* 一台jmeter，查询300W次，TPS：14879.5
  ![](/assets/QQ截图20160929175523.png)

#### 根据索引键cust\_number查询数据的效率

* 一台jmeter，查询300W次，太慢，终止了。。。TPS：10.5
  ![](/assets/QQ截图20160930084504.png)

#### 根据普通字段查询数据的效率

该字段，非分片键，非索引键

* 一台jmeter，查询300W次，太慢，终止了。。。TPS：10.5
  ![](/assets/QQ截图20160930084335.png)

