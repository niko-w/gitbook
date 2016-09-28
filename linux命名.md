### 基本命令

#### tail

> tail命令从文件指定点开始将文件写到标准输出流，使用**tail命令的-f选项**可以方便的查阅正在改变的日志文件,`tail -f filename`会把filename里最尾部的内容显示在屏幕上,并且不但刷新,使你看到最新的文件内容.

##### 命令格式

`tail [ -f ] [ -c Number | -n Number | -m Number | -b Number | -k Number ] [ File ]`
###### 参数解释：
-f 该参数用于监视File文件增长。
-c Number 从 Number 字节位置读取指定文件
-n Number 从 Number 行位置读取指定文件。
-m Number 从 Number 多字节字符位置读取指定文件，比方你的文件假设包括中文字，假设指定-c参数，可能导致截断，但使用-m则会避免该问题。
-b Number 从 Number 表示的512字节块位置读取指定文件。
-k Number 从 Number 表示的1KB块位置读取指定文件。
File 指定操作的目标文件名称
上述命令中，都涉及到number，假设不指定，默认显示10行。Number前面可使用正负号，表示该偏移从顶部还是从尾部開始计算。
tail可运行文件一般在\/usr\/bin\/以下。

