#### 柔性数组( Flexible Array )


	柔性数组(Flexible Array)：也叫伸缩性数组、可变长数组，反映了C语言对精炼代码的极致追求。这种代码结构产生于
	
	对动态结构体的需求。比如我们需要在结构体中存放一个动态长度的字符串，这时候，柔性数组可以大显身手了。
	

<br>

	注意：经测试在 VC++6.0 及 VS2013 下柔性数组必须放在结构体最后。而且，在 VS2013 下会给出这样的警告：
	
		 warning C4200: 使用了非标准扩展 : 结构/联合中的零大小数组当 UDT 包含大小为零的数组时，无法生成
		 
		 复制构造函数或副本赋值运算符
	


<br>

#### 代码 

```cpp

		# include <iostream>
		using namespace std;
		
		
		//柔性数组
		struct A
		{
			int a;
			int b;
			char array[];                //必须是在结构体的最后，也可以这样 char array[0];
		};
		
		int main()
		{
			cout << sizeof(A) << endl;   //输出 sizeof(A): 8 字节，正好是 a+b 的和
		
			char* src = "FlexibleArray";
		
			A* FA = (A*)malloc(sizeof(A)+strlen(src) + 1);
		
			FA->a = 1;
			FA->b = 2;
			strcpy(FA->array, src);
		
			cout << "&FA->a：    " << &FA->a << endl;      //&FA->a：    00D8A3B0
			cout << "&FA->b：    " << &FA->b << endl;      //&FA->b：    00D8A3B4
			cout << "&FA->array：" << &FA->array << endl;  //&FA->array：00D8A3B8
		
			cout << "FA->a：" << FA->a << endl;            //FA->a：1
			cout << "FA->b：" << FA->b << endl;            //FA->b：2
			cout << "FA->array：" << FA->array << endl;    //FA->array：FlexibleArray
		
			system("pause");
			return 0;
		}

```


