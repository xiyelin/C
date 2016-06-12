
----------------------------------------------------------------------------------------------------------------------------------------

第一题：以下程序的结果是什么？

```c
            int i = 1;

            int main()
            {
                int i = i;

                return 0;
            }

            A: main()函数里的i是一个未定义值        B: main()函数的i为1
            C: 编译器不允许这种写法                 D: main()里i的值为0
            
```
            
    分析：  
            在VC++ 6.0 中编译 -->  warning C4700: local variable 'i' used without having been initialized
            在 VS 2013 中编译 -->  error C4700: 使用了未初始化的局部变量“i”

            当main()函数里的i从定义开始，外部的全局变量i就已经被屏蔽掉，所以main()函数里作为右值的i的值不会0也不会是1，
            与外部的i无关。而是一个未定义的符号。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第二题：以下程序的输出结果是什么？

```c
            #include<stdio.h>

            int main()
            {
                int arr[]={11,12,13,14,15};
                int *ptr = arr;

                *(ptr++) += 100;

                printf("%d %d\n",*ptr,*(++ptr));

                return 0;
            }
            
            A:13 13         B：112 13       C ：12 12       D：12 13
            
```

    分析：
            考点：前置++、后置++，指针访问数组以及printf()函数参数压栈顺序；
            
            刚开始ptr指向11，然后执行*(ptr++) += 100;因为是后置++，所以此时第一个元素的值变成了111，然后ptr指向元素12；
            接着进入了printf()函数，这时参数按照从右向左的顺序依次执行并压栈，所以ptr先指向了元素13，因为输出为 13,13。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第三题：以下代码说法正确的是:

```c
            #include<stdio.h>

            int main(void)
            {
                char aChar;
                int aInt;

                aInt = aChar = -120;

                printf("%d\n",aInt);

                return 0;
            }
            
            A:一定输出-120      B:一定不能输出-120
            C:可能输出-120      D:输出%d

```
            
    分析：
            首先，在不同的编译器中默认的char类型可能是有符号的也可能是无符号的；signed char的取值范围是[-128, +127]，
            而unsigned char的取值范围是[0, +255]，所以，此时如果是有符号的char那么aChar的值为-120，如果默认是无符号的
            则aChar的值为+136；其次32位平台下将一个8位的aChar赋值给32位的aInt，究竟是放在高八位还是第八位，取决于系统
            的存储模式，分为大端存储和小端存储。因此，最后的结果可能是-120，但不确定。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第四题：下面这个程序的输出结果是什么？

```c
            #include <stdio.h>

            int main()
            {
                int i=43;

                printf("%d\n",printf("%d",printf("%d",i)));

                return 0;
            }

```
            
    分析：
            本程序将输出4321。原因在于先输出i的值为43然后紧接着输出printf的返回值!而printf的返回值为输出的字符的个数！
            所以呢再执行完最里面的printf("%d",i)打印43之后，接着打印printf("%d",43)这句话的返回值即2，然后在打印
            printf("%d",2)的返回值即1.所以最后结果为4321。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第五题：下面这个程序运行后，m和n的值是多少？

```c
            #include <stdio.h>
            
            int main() 
            {  
                int a=4,b=3,c=2,d=1,m=2,n=2;
            
                (m=a<b)&&(n=c>d);
            
                printf("m=%d,n=%d",m,n);
            
                return 0;
            }
            
```

    分析：
            m=0,n=2 第一个m为0我相信大家这个都没什么问题，至于第二个n为什么是2，有人可能会想c>d不是成立吗？
            那应该返回真也就是1给n,为什么还是2呢？原因在于&&和||运算符都是短路运算符，即编译器一旦发现与整
            体表达式无关，那么求值立刻终止。所以在计算出a<b为假以后，那么&&右边的表达式真假已没有意义了。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第六题： 以下程序的输出结果是什么？

```c
            #include <stdio.h>
            
            int main()  
            {
            	int i;
           
            	i = 10;
            
            	printf("i : %d\n",i);
            	printf("sizeof(i++) is: %d\n",sizeof(i++));
            	printf("i : %d\n",i);
            
            	return 0;
            }
            
```
            
    分析：
            输出的三个值会是 10、4、11吗？如果你也是这个答案那就错了!
            
            第一个10没问题，第二个是求int类型数据的大小，也是4，也没问题。问题在于在sizeof()里还有个副作用++,
            难道这个没有执行吗？怎么还可能是10呢？原因在于sizeof是一个关键字，而非函数！i++在编译器看来是可以
            在运行前也就是编译的时候就确定了的。故sizeof(i++)其实就是4。更不会有i++了。所以最后结果为10、4、10。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第七题：gets()函数，请找出下面代码里的问题：

```c
            #include<stdio.h> 
            
            int main(void) 
            { 
                char buff[10]; 
                memset(buff,0,sizeof(buff)); 
             
                gets(buff); 
             
                printf("\n The buffer entered is [%s]\n",buff); 
             
                return 0; 
            }
            
```
            
    分析：
            此程序的buff只有十个字节，出去最后一个字符串结束的标志，最多读取9个字符为合法；然后这里的gets()则不会检查是否会
            产生溢出的可能，所以这里可能会溢出，导致程序崩溃；建议使用fgets()函数避免这个问题。
            
            fgets()函数--->从文件结构体指针stream中读取数据，每次读取一行。读取的数据保存在buf指向的字符数组中，每次最多读
                           取bufsize-1个字符（第bufsize个字符赋'\0'），如果文件中的该行，不足bufsize个字符，则读完该行就结
                           束。如若该行（包括最后一个换行符）的字符数超过bufsize-1，则fgets只返回一个不完整的行，但是，缓冲
                           区总是以NULL字符结尾，对fgets的下一次调用会继续读该行。函数成功将返回buf，失败或读到文件结尾返回
                           NULL。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第八题：strcpy()函数，下面是一个简单的密码保护功能，你能在不知道密码的情况下将其破解吗？

```c
            #include<stdio.h> 
     
            int main(int argc, char *argv[]) 
            { 
                int flag = 0; 
                char passwd[10]; 
             
                memset(passwd,0,sizeof(passwd)); 
             
                strcpy(passwd, argv[1]); 
             
                if(0 == strcmp("LinuxGeek", passwd)) 
                { 
                    flag = 1; 
                } 
             
                if(flag) 
                { 
                    printf("\n Password cracked \n"); 
                } 
                else 
                { 
                    printf("\n Incorrect passwd \n"); 
                }
                
                return 0;
            }
   
```
   
    分析：
            破解上述加密的关键在于利用攻破strcpy()函数的漏洞。所以用户在向“passwd”缓存输入随机密码的时候并没有提前检查
            “passwd”的容量是否足够。所以，如果用户输入一个足够造成缓存溢出并且重写“flag”变量默认值所存在位置的内存的长
            “密码”，即使这个密码无法通过验证，flag验证位也变成了非零，也就可以获得被保护的数据了。
            
            要避免这样的问题，建议使用 strncpy()函数。
            最近的编译器会在内部检测栈溢出的可能，所以这样往栈里存储变量很难出现栈溢出。在我的gcc里默认就是这样，所以我
            不得不使用编译命令‘-fno-stack-protector’来实现上述方案。

----------------------------------------------------------------------------------------------------------------------------------------
<br>
第九题：处理printf()的参数，下面代码会输出什么？

```c
            #include<stdio.h> 
 
            int main(void) 
            { 
                int a = 10, b = 20, c = 30; 
                printf("\n %d..%d..%d \n", a+b+c, (b = b*2), (c = c*2)); 
             
                return 0; 
            }
            
```
            
    分析：
            printf()函数的参数执行顺序是从右向左依次执行并压栈，所以先计算（c = c * 2 ），然后计算（ b = b * 2 ），最后
            计算（ a+b+c ）；最后输出的结果为 110..40..60


----------------------------------------------------------------------------------------------------------------------------------------

