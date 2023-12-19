---
layout: detail
type : 2
keyword :     
title: memory map
description: 
---

## 内存映射

内存映射（Memory Mapping）是一种将文件的内容直接映射到进程的地址空间中的技术。这样做可以使得文件的内容可以像内存一样被访问，从而可以通过内存操作来读取和写入文件，而无需进行显式的文件I/O操作。在C++中，可以使用操作系统提供的相关API来进行内存映射，比如在Linux下可以使用mmap函数

好处主要有以下几点：

提高文件读写效率
内存映射技术可以将文件的内容直接映射到进程的地址空间中，从而可以像访问内存一样访问文件的内容。避免频繁的文件I/O操作，提高文件读写效率。

方便文件的随机访问
内存映射技术可以将文件的任意部分映射到内存中，可以方便地进行文件的随机访问。通过指针可以直接访问文件的任意位置，无需像传统的文件I/O操作那样需要先定位文件指针。

简化代码实现
内存映射技术可以将文件的内容直接映射到内存中，通过内存操作来读写文件，简化代码的实现。不需要使用繁琐的文件I/O操作，可以直接使用内存操作来读写文件。

共享内存
内存映射技术可以将文件映射到多个进程的地址空间中，实现共享内存。这样可以方便地进行进程间通信，比如实现进程间共享数据等。


## 代码实现

```c
#include <iostream>
#include <sys/mman.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <unistd.h>

int main() {
    int fd = open("file.txt", O_RDWR); // 打开文件
    struct stat sb;
    fstat(fd, &sb); // 获取文件信息

    char *addr = (char *)mmap(NULL, sb.st_size, PROT_READ | PROT_WRITE, MAP_SHARED, fd, 0); // 将文件映射到内存
    close(fd); // 关闭文件

    // 现在文件的内容已经映射到了内存中的addr指针所指向的位置
    // 可以通过addr指针来访问文件的内容
    std::cout << "File content: " << addr << std::endl;

    // 修改文件内容
    addr[0] = 'H';
    addr[1] = 'i';

    // 取消内存映射
    munmap(addr, sb.st_size);
    
    return 0;
}
```

使用 memory map 的时候需要小心处理数据的一致性和同步问题