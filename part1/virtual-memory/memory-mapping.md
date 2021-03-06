4.8 内存映射

内存映射中的“映射”主要指在一些实体\(文件，设备，物理内存\)和虚拟内存 region 之间建立联系。当 loader 填充进程的地址空间后，进程向操作系统请求某个页，这时候操作系统从文件系统把内容“投射”到进程的地址空间中---这就是内存映射的一个例子。

系统调用 mmap 就是用来做各种类型的内存映射的。调用它我们需要在第二章中介绍的同样的几个步骤。表 4-1 展示了该系统调用的参数。

_**Table 4-1**. mmap 系统调用_

| REGISTER | VALUE | MEANING |
| :--- | :--- | :--- |
| rax | 9 | 系统调用编号 |
| rdi | addr | 操作系统尝试从这个指定的地址开始映射内存页。该地址应对应页的起始位置。传 0 表示操作系统可以选择任意起始位置。 |
| rsi | len | 内存 region 大小 |
| rdx | prot | 保护 flag\(read, write, execute...\) |
| r10 | flags | 公用 flag\(共享还是私有还是匿名页，等等\) |
| r8 | fd | 可选的需要映射的文件，该文件应该已经被 open 过了 |
| r9 | offset | 文件中的偏移 |

调用 mmap 之后，rax 将持有一个指向新分配的内存页的指针。

