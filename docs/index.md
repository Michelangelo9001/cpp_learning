## 1 程序基本结构

```cpp
#include<iostream>

int main(){
	std::cout<<"hello cpp"<<std::endl;
	return 0;
}
```

## 2 分支结构

### 2.1 if语句

```cpp
int i=1;
if(i==0){
	std::cout<<"no"<<std::endl;
}else if(i==1){
	std::cout<<"yes"<<std::endl;
}else{
	std::cout<<"unknown"<<std::endl;
}
```

### 2.2 switch语句

```cpp
int i=0;
switch(i){
case 0:
	std::cout<<"no"<<std::endl;
	break;
case 1:
	std::cout<<"yes"<<std::endl;
	break;
default:
	std::cout<<"unknown"<<std::endl;
	break;
}
```

> [!IMPORTANT]
>
> `switch` 只能用于整型（`int`、`char`、`bool`、`enum` 等）或能隐式转换为整型的类型，字符串适合使用if语句。

## 3 循环结构

### 3.1 for循环

```cpp
//适合已知循环次数
for(int i=0;i<10;i++){
	std::cout<<i<<std::endl;
}
```

### 3.2 while循环

```cpp
//适合未知循环次数，只知道循环条件
int x=0;

while(x<5){
	std::cout<<x<<std::endl;
	x++;
}
```

### 3.3 do while循环

```cpp
int x=1;

do{
	std::cout<<x<<std::endl;
	x++;
}while(x<0);
```

### 3.4 break和continue

```cpp
//break结束当前循环
for(int i=0;i<10;i++){
	if(i==5){
		break;
	}
	std::cout<<i<<std::endl;
}
//continue跳过此次循环
for(int i=0;i<10;i++){
	if(i==5){
		continue;
	}
	std::cout<<i<<std::endl;
}
```

## 4 函数

### 4.1 基础用法

```cpp
#include<iostream>

//函数声明写在main函数前
void print_add(int x,int y);

int main(){
	int a=0;
	int b=1;
	print_add(a,b);
	return 0;
}

//函数定义在main之后
void print_add(int x,int y){
	std::cout<<x+y<<std::endl;
}
```

### 4.2 引用传递

```cpp
void add_one(int& x){
	x+=1;
}

int a=0;
add_one(a);//引用传递可以修改原变量，不同于值传递获得的是副本
std::cout<<a<<std::endl;

//项目中常用常量引用传递，不允许函数内部修改变量
void add_one(const int& x){
	x+=1;		//编译报错，不能修改const变量
}
```

### 4.3 函数重载

函数名相同，函数参数类型不同，编译器会自动匹配。

```cpp
void print_add(int x,int y){
	std::cout<<x+y<<std::endl;
}

void print_add(double x,double y){
	std::cout<<x+y<<std::endl;
}

print_add(1,2);
print_add(1.0,2.0);
```

### 4.4 默认参数

```cpp
void print_add(int x,int y=1);

void print_add(int x,int y){
	std::cout<<x+y<<std::endl;
}

print_add(1);
print_add(1,2);
```

> [!IMPORTANT]
>
> 缺省参数必须在普通参数右侧，缺省值写在声明处，定义处不可重复定义。

## 5 指针变量

### 5.1 基础用法

指针是一种特殊的数据类型，在64位Linux系统中占用8个字节。指针存储变量的内存地址，可以使用取地址符`&`赋值。

```cpp
int a=0;
int* p=&a;
std::cout<<*p<<std::endl;
```

### 5.2 指针与常量

```cpp
const int* p
//常量指针，不能通过指针修改变量的值
int* const p
//指针常量，指针不能指向其他变量
```

## 6 数据类型

### 6.1 数组

- **定义与访问**

```cpp
int arr1[5]={1,2,3,4,5};
int arr2[5] = {1, 2};				//未定义元素自动补全为0
int arr3[] = {1, 2, 3, 4, 5};		//编译器自动计算数组大小
int arr4[5]={};						//所有元素为0
std::cout<<arr[0];
```

- **遍历**

```cpp
for(int i=0;i<5;i++){
	std::cout<<arr[i];
}
```

- **数组与指针**

```cpp
int* p=arr;
if(p==&arr[0]){
	std::cout<<"yes"<<std::endl;		//输出yes，说明arr等价于数组首元素地址
}
if(*(p+1)==p[1]){
	std::cout<<"yes"<<std::endl;		//输出yes
}
```

- **数组与函数**

数组作为参数时，使用数组语法和指针语法完全等价，传递的都是首元素地址。

```cpp
void print_arr(int arr[],int size);
void print_arr(int* arr,int size);
```

### 6.2 vector容器

`vector`是动态数组，在项目中比普通数组更常用。

- **定义**

```cpp
#include <vector>

std::vector<int> v;			//空的整数vector
std::vector<int> v(5);		//5个元素，默认为0
std::vector<int> v(5,10);	//5个元素，全部为10
std::vector<int> v={1,2,3,4,5};
```

- **基本操作**

```cpp
//末尾添加元素
v.push_back(6);

//获取末尾元素
int a=v.back();

//获取长度
int len=v.size();

//访问元素方式与数组一致
std::cout<<v[6]<<std::endl;
```

### 6.3 string字符串

- **定义和初始化**

```cpp
#include<string>

std::string s="hello";
std::string s("hello");
std::string s(5,'a');
```

- **字符串输入**

```cpp
std::cin>>s;
std::getline(std::cin,s);
```

> [!IMPORTANT]
>
> `cin`遇到空格停止，输入带空格的字符串需要使用`getline`方法。

- **获取长度**

```cpp
if(s.empty()){
	std::cout<<"string is empty";
}

s.size();
```

- **其他常见用法**

```cpp
//访问字符串
std::cout<<s[0];
s[0]='A';
s.front();
s.back();

//字符串拼接
std::string result=first+" "+second;
s.append(" world");
```

- **其他字符串表示方法**

  - 字符数组

    ```cpp
    char s[6] = "hello";
    char s[] = {'h', 'e', 'l', 'l', 'o', '\0'};
    std::cout<<s<<std::endl;
    ```

    > [!IMPORTANT]
    >
    > C风格字符串的最后一个元素是空字符`'\0'`，因此数组长度通常比真实字符串长度大1，使得字符数组可以直接使用`cout`输出。

  - 字符指针

    ```cpp
    const char* s = "hello";
    std::cout << s;
    std::cout << s[0];
    ```

### 6.4 struct结构体

```cpp
struct Point{
	double x;
	double y;
};

Point p={1.0,2.0};

double distanceToOrigin(const Point& p){
	return sqrt(p.x*p.x+p.y*p.y);
}
```