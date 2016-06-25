---------------------------------------

* [Memcpy](#memcpy)
* [Memmove](#memmove)

---------------------------------------



#### Memcpy

	c和c++使用的内存拷贝函数，memcpy函数的功能是从源src所指的内存地址的起始位置开始拷贝n个字节
	
	到目标dest所指的内存地址的起始位置中。函数返回指向dest的指针。
	
<br>

	注意：1.source和destin所指的内存区域可能重叠，但是如果source和destin所指的内存区域重叠,那么
		  
		   这个函数并不能够确保source所在重叠区域在拷贝之前不被覆盖。而使用memmove可以用来处理重叠
		 
		   区域。函数返回指向destin的指针.
		 
		 
		 2.如果目标数组destin本身已有数据，执行memcpy（）后，将覆盖原有数据（最多覆盖n）。如果要
		 
		   追加数据，则每次执行memcpy后，要将目标数组地址增加到你要追加数据的地址。
		 
		  
		 3.source和destin都不一定是数组，任意的可读写的空间均可。
		  

#### code

```cpp

		void* Memcpy(void* dst, const void* src, int n)     //src加const,只读，防止被意外修改，
		{
			assert(dst);
			assert(src);
			assert(n >= 0);
		
			char* cdst = (char*)dst;                        //内存的拷贝是一个字节一个字节的拷贝
			char* csrc = (char*)src;
		
			while (n--)
				*cdst++ = *csrc++;
		
			return dst;
		}
		
		
```

<br>

#### strcpy和memcpy主要有以下3方面的区别:

	1.复制的内容不同。strcpy只能复制字符串，而memcpy可以复制任意内容，例如字符数组、整型、结构体、类等。
	
	2.复制的方法不同。strcpy不需要指定长度，它遇到被复制字符的串结束符"\0"才结束，所以容易溢出。memcpy
	
	  则是根据其第3个参数决定复制的长度。
	 
	3.用途不同。通常在复制字符串时用strcpy，而需要复制其他类型数据时则一般用memcpy。
	
	
<br>
<br>

#### Memmove

	memmove用于从src拷贝count个字符到dest，如果目标区域和源区域有重叠的话，memmove能够保证源串在被覆盖之前将重
	
	叠区域的字节拷贝到目标区域中。但复制后src内容会被更改。但是当目标区域与源区域没有重叠则和memcpy函数功能相同。
	

<br>


#### code

```cpp

		void* Memmove(void* dst, const void* src, size_t count)
		{
			assert(dst);
			assert(src);
		
			char* chsrc = (char*)src;
			char* chdst = (char*)dst;
		
			if (chdst<chsrc || chdst >(chsrc + count))         //内存不重叠的情况，从前往后，从后往前后可以
			{
				while (count--)
				{
					*chdst = *chsrc;
					++chdst;
					++chsrc;
				}
			}
			else                                               //内存重叠时，从后往前拷贝
			{
				chsrc += (count - 1);
				chdst += (count - 1);
		
				while (count--)
				{
					*chdst = *chsrc;
					--chdst;
					--chsrc;
				}
			}
		
			return dst;
		}
		
		
		
```



