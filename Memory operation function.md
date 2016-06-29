-----------------------------------------------------------------------------------------------------------------------------------
    
#### No.1.
	malloc/calloc/free: malloc和calloc都可以分配内存区，但malloc一次只能申请一个内存区，calloc一次可以申请多个内存区．另外
    calloc会把分配来的内存区初试化为０，malloc不会进行初始化。
           
    free 可以释放由malloc或calloc等内存分配函数分配的内存．当程序很大时，期间可能要多次动态分配内存，如果不及时释放的话，程
    序将要占用很大内存。要注意，如果ptr所指内存已被释放或是未知的内存地址，则可能有无法预期的情况发生。若参数为NULL，则free
    不会有任何作用。

-----------------------------------------------------------------------------------------------------------------------------------

#### No.2.
    memset: 将s所指向的某一块内存中的前n个字节的内容全部设置为ch指定的ASCII值， 第一个值为指定的内存地址，块的大小由第三个参
    数指定，这个函数通常为新申请的内存做初始化工作， 其返回值为指向s的指针。
    
    函数原型为：void *memset(void *s, int ch, size_t  n);

<br>

```c

/*
**函数解释：将s中前n个字节 （typedef unsigned int size_t ）用 ch 替换并返回 s 。
**memset：作用是在一段内存块中填充某个给定的值，它是对较大的结构体或数组进行清零操作的**一种最快方法。
*/
void *memset(void *s, int ch, size_t n)
{
     assert(s);
      
     void *dst = s;
      
     while (n--)
     {
          *(char *)dst = ch;
          dst = (char *)dst + 1;
     }
      
     return s;
}


```

-----------------------------------------------------------------------------------------------------------------------------------

No.3.
    memncmp: memcmp是比较内存区域buf1和buf2的前n个字节。该函数是按字节比较的。
    
    函数原型为：int memset(const void *dst, const void *src, size_t  n);


```c


int memcmp(const void *dst, const void *src, size_t n)
{
     assert(dst);
     assert(src);
      
     /*
     **逐字节比较，比较的字节数小于等于n.
     */
     while ((n) && (*(char *)dst == *(char *)src))
     {
          dst = (char *)dst + 1;
          src = (char *)src + 1;
          n--;
     }
     if ((!n) && (!*(char *)src))
     {
          return (0);
     }
     else if ((*(char *)dst - *(char *)src) < 0)
     {
          return (1);
     }
     else
          return (-1);
}


```

-----------------------------------------------------------------------------------------------------------------------------------

No.4.
    memcpy: memcpy函数的功能是从源src所指的内存地址的起始位置开始拷贝size个字节到目标dst所指的内存地址的起始位置中。
        
  
```c


void* memcpy(void *dst, const void *src, size_t size)
{
     assert(dst);
     assert(src);
      
     void* ret = dst;
      
     while (size--)
     {
          *(char *)dst = *(char *)src;
          dst = (char *)dst + 1;
          src = (char *)src + 1;
     }
      
     return ret;
}     
   
        
```
-----------------------------------------------------------------------------------------------------------------------------------

No.5.
    memmove: memmove用于从src拷贝size个字符到dst，如果目标区域和源区域有重叠的话，memmove能够保证源串在被覆盖之前将重叠区域的字
    节拷贝到目标区域中。但复制后src内容会被更改。但是当目标区域与源区域没有重叠则和memcpy函数功能相同。


```c


void *my_memmove(void *dst, const void *src, size_t size)
{
     assert(dst);
     assert(src);
      
     void* ret = dst;
      
     /*
     **发生内存重叠时执行if语句，不重叠时相当于memcpy，执行else。
     */
     if ((dst > src) && ((char *)dst < (char *)src + size))
     {
          while (size--)
          {
               *((char *)dst + size) = *((char *)src + size);
          }
     }
     else
     {
          while (size--)
          {
               *(char *)dst = *(char *)src;
               dst = (char *)dst + 1;
               src = (char *)src + 1;
          }
     }
      
     return ret;
}


```

-----------------------------------------------------------------------------------------------------------------------------------


