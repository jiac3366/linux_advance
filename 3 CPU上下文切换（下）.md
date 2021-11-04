---
title: CPU上下文切换（下）
categories:
  - Linux性能优化
toc: true 
---

- **vmstat**用来分析系统的内存使用情况,也常用来分析CPU 上下文切换和中断的次数
  ![image-20211013203206540](C:\Users\46304\AppData\Roaming\Typora\typora-user-images\image-20211013203206540.png)

  - cs（context switch）是每秒上下文切换的次数。 
  - in（interrupt）则是每秒中断的次数。 
  - r（Running or Runnable）是就绪队列的长度，也就是正在运行和等待 CPU 的进程数。 若大于CPU数说明存在CPU竞争
  - b（Blocked）则是处于不可中断睡眠状态的进程数 
  - us(user) 
  - sy 系统CPU使用率 

- 进一步每个进程的详细情况 使用**pidstat**
  pidtstat -w 5 隔5s输出一组数据  单位: 次/秒
  -w 参数表示输出进程切换指标，而 -u 参数则表示输出 CPU 使用指标
  **默认显示进程指标数据，加-t才输出线程指标** ——pidstat -wt 1

  - cswch，自愿上下文切换，eg: 资源不足
  - nvcswch非自愿上下文切换，eg:时间片耗尽

- **sysbench** 是一个多线程的基准测试工具，一般用来评估不同系统参数下的数据库负载情况
  sysbench --threads=10 --max-time=300 threads run

  ![image-20211013204314491](C:\Users\46304\AppData\Roaming\Typora\typora-user-images\image-20211013204314491.png)

-  pidstat 只是一个进程的性能分析工具，而中断发生在内核态，怎样才能知道中断发生的类型呢？

