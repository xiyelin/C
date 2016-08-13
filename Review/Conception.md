## C语言常见的基础概念

-------------------------------------------------


### 1.static在C和C++里各代表什么含义？

	
	C语言中：

- [x] ` 修饰局部变量 `
	
	局部静态变量-->生命周期：伴随整个程序运行周期；存储位置：存在静态区；
	static局部变量在所处模块在初次运行时进行初始化工作，且只操作一次；
	特点: static局部变量的”记忆性”与生存期的”全局性”；

- [x] ` 修饰全局变量/函数 `

	全局静态变量/静态函数-->指对变量或函数的作用域仅局限于本文件(所以又称内部函数)；
	外部(全局)变量, 不论是否有static限制, 它的存储区域都是在静态存储区,生存期都是全局的；							  使用内部函数的好处是：不同的人编写不同的函数时，不用担心自己定义的函数，是否会与其它文件中的函数同名。

<br>

	在C++中：除了具备C语言中的作用，它还有如下作用：
	
- [x] ` 修饰成员变量和成员方法 `

	静态数据成员和静态成员方法---> 属于一个类而不是属于此类的任何特定对象的变量和函数；
	静态成员函数没有this指针，调用时在函数名前加上类名即可；
	静态成员变量在类外初始化，初始化时加上类名；

<br>


### 2.const在C/C++中的用法：

- [x] ` const 修饰局部变量，函数参数和函数的返回值 `

	只读变量，在只读区为其开辟空间，注意它是一个变量，而不是常量；
	数组的定义必须是常量；而在C++中，const正常情况下是看成编译期的常量,编译器并不为const分配空间,
	只是在编译的时候将期值保存在名字表中，所以在C++中const修饰的量可以用在数组的定义中。

- [x] ` const 修饰成员函数，成员变量 `
	
	1.非const的成员变量既可以调用const类型的成员函数，也可以调用非const类型的成员函数； 
	2.const类型的成员变量只能调用const类型的成员函数； 
	3.非const类型的成员函数内既可以调用非const类型的成员函数，又可以调用const类型的成员函数； 
	4.const类型的成员函数只能调用const类型的成员函数；

<br>

### 3.volatile关键的作用：

	为提高存取速度，编译器优化时有时会先把变量读取到一个寄存器中；以后，再取变量值时，就直接从寄存器中取值；
	将一个变量声明为volatile时，就是告诉编译器，我这个变量的值随时可能改变，与该变量相关的操作不可以优化，每
	次读取该变量是都要从内存中去取。-----------(保持内存可见性，尤其是在多线程情况下容易出错)

<br>

### 4.new&delete 和malloc&free的区别：

<https://github.com/xiyelin/CPP/blob/master/malloc_free%20%26%20new_delete.md>

<br>


### 5.指针和数组的区别：

	指针在32位平台下占4个字节，而数组的大小和存在其中元素的类型以及元素的个数有关；
	
	对于编译器来说，指针变量里边存储的任何东西都将被视作地址；而数组里边保存的是一系列相同类型的数据；
	
	指针必须通过间接的方式访问其变量的数据，而数组可以直接通过下标来访问；
	
	数组名和数组首元素的地址相同，所以通过下标访问数组元素其实底层就相当于是指针的首地址加偏移量；
	
	指针相比于数组来说，更加灵活，但也更加容易出错，指针可以指向任何一个地方；
	
	当数组名作为函数参数进行传递时，该数组自动退化该类型的指针；
	
	指针和数组都可以被一个字符串常量进行初始化，初始化指针时所指向的字符串被定义为只读，不能改变；
	

<br>

### 6.














	
	
	
	
	













