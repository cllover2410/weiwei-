

## 1.1 系统性能信息模块psutil
psutil是一个跨平台库（http://code.google.com/p/psutil/），能够轻松实现获取系统运行的进程和系统利用率（包括CPU、内存、磁盘、网络等）信息。它主要应用于系统监控，分析和限制系统资源及进程的管理。它实现了同等命令行工具提供的功能

```python
import psutil # psutil大小单位一般都采用字节
mem = psutil.virtual_memory()
mem.total，mem.used # 获取当前物理内存总大小及已使用大小
```

### 1.1.1 获取系统性能信息
- User Time，执行用户进程的时间百分比；
- System Time，执行内核进程和中断的时间百分比；
- Wait IO，由于IO等待而使CPU处于idle（空闲）状态的时间百分比；
- Idle，CPU处于idle状态的时间百分比。

我们使用Python的psutil.cpu_times()方法可以非常简单地得到这些信息，同时也可以获取CPU的硬件相关信息，比如CPU的物理个数与逻辑个数，具体见下面的操作例子：

```python
import psutil
psutil.cpu_times() #使用cpu_times方法获取CPU完整信息，需要显示所有逻辑CPU信息。
psutil.cpu_times(percpu=True) #指定方法变量percpu=True即可，如
    >>> scputimes（user=38.039999999999999， nice=0.01，system=110.88， idle=177062.59， iowait=53.399999999999999，irq=2.9100000000000001， softirq=79.579999999999998，steal=0.0， guest=0.0）
psutil.cpu_times().user #获取单项数据信息，如用户user的CPU时间比38.0
psutil.cpu_count() #获取CPU的逻辑个数，默认logical=True4
>>>psutil.cpu_count(logical=False) #获取CPU的物理个数
```