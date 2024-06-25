# 基本知识

### Go语言特点

静态强类型：在编译时就能确定变量的数据类型，并且对于不同类型的数据有严格的类型检查

编译型：需要将源代码转换成机器语言或者字节码

并发型：指语言内置了处理并发的机制，允许程序中同时执行多个任务或操作

垃圾回收：它会自动检测和释放不再使用的内存，避免了内存泄漏和野指针等问题

## 变量和数据结构

### 基础语法

1、Go 语言中变量的声明必须使用空格隔开

2、Sprintf 根据格式化参数生成格式化的字符串并返回该字符串

​      Printf 根据格式化参数生成格式化的字符串并写入标准输出

```go
func main() {
   // %d 表示整型数字，%s 表示字符串
    var stockcode=123
    var enddate="2020-12-31"
    var url="Code=%d&endDate=%s"
    var target_url=fmt.Sprintf(url,stockcode,enddate)
    fmt.Println(target_url)
    fmt.Printf(url,stockcode,enddate)
}
```

### 基本类型变量

布尔型：b := true

数字型：**uint8**、**uint16**、**uint32**、**uint64**、**int8**、 **int16**、**int32**、**int64**

字符串：不可变，如果基本是英文，每个字符占 1 byte，和 ASCII 编码是一样的，非常节省空间，如果是中文，一般占3字节

```go
//字符串的长度可以使用 len() 函数获取，它返回的是字符串的字节数
    str := "Hello, 世界"
    fmt.Println(len(str)) // 输出: 13
//字符串可以使用索引访问单个字节，并且可以使用切片操作符访问子字符串
    fmt.Println(str[0]) // 输出: 72 ('H' 的 ASCII 码)
    fmt.Println(substr) // 输出: 世
//要修改字符串，通常需要创建一个新的字符串
    newStr := "H" + str[1:]
    fmt.Println(newStr) // 输出: Hello, 世界
//可以使用 + 运算符或 fmt.Sprintf 函数进行字符串拼接
    str := str1 + ", " + str2 + "!"
    fmt.Println(str) // 输出: Hello, World!
// 检查是否包含子串
fmt.Println(strings.Contains(str, "World")) // 输出: true

// 替换子串
newStr := strings.Replace(str, "World", "Go", 1)
fmt.Println(newStr) // 输出: Hello, Go!

// 分割字符串
parts := strings.Split(str, ", ")
fmt.Println(parts) // 输出: [Hello World!]

// 转换大小写
fmt.Println(strings.ToUpper(str)) // 输出: HELLO, WORLD!
fmt.Println(strings.ToLower(str)) // 输出: hello, world!
// 数字转字符串
i := 123
str := strconv.Itoa(i)
fmt.Println(str) // 输出: 123

// 字符串转数字
str = "456"
num, err := strconv.Atoi(str)
```

### 复合类型变量

```go
//Go语言
var arr [5]int = [5]int{1,2,3,4,5}
var slice[]int = []int{1,2,3,4,5}
var mymap map[string]int = map[string]int{"a":1,"b":2}
var mystruct struct{Name string;Age int} = struct{Name string;Age int}{"Json",30}
```

### 切片

```go
slice1 := make([]float32, 0) // 长度为0的切片
slice2 := make([]float32, 3, 5) // [0 0 0] 长度为3容量为5的切片
fmt.Println(len(slice2), cap(slice2)) // 3 5
slice2 = append(slice2, 1, 2, 3, 4) // [0, 0, 0, 1, 2, 3, 4]
sub1 := slice2[3:] // [1 2 3 4]
sub2 := slice2[:3] // [0 0 0]
sub3 := slice2[1:4] // [0 0 1]
combined := append(sub1, sub2...) // [1, 2, 3, 4, 0, 0, 0]
```

### 字典

```go
// 仅声明
m1 := make(map[string]int)
// 声明时初始化
m2 := map[string]string{
	"Sam": "Male",
	"Alice": "Female",
}
```

### 指针

```go
// Go语言
var ptr *int = &num

// C++
int* ptr = &num;
```

### 函数指针

```go
// Go语言
var funcVar func(int) int = func(x int)int {return x*x}

// C++
int square(int x) { return x * x; }
int (*funcVar)(int) = square;
```

### 链表

```go
// 创建一个新的链表
myList := list.New()

// 向链表中添加元素
myList.PushBack(1)
myList.PushFront(0)

// 遍历链表并打印元素值
for e := myList.Front(); e != nil; e = e.Next() {
    fmt.Println(e.Value)
}

// 获取链表的长度并打印
fmt.Println("Length:", myList.Len())

// 删除链表中的第一个元素
myList.Remove(myList.Front())

// 遍历链表并打印元素值
for e := myList.Front(); e != nil; e = e.Next() {
    fmt.Println(e.Value)
}
```

## 分支语句

### if else

```go
// 可以简写为：
if age := 18; age < 18 {
	fmt.Printf("Kid")
} else {
	fmt.Printf("Adult")
}
```

### switch

```go
switch gender {
case FEMALE:
	fmt.Println("female")
	fallthrough
case MALE:
	fmt.Println("male")
	fallthrough
default:
	fmt.Println("unknown")
}
```

### for循环

```go
for i := 0; i < 10; i++ {
	if sum > 50 {
		break
	}
	sum += i
}
//数组
nums := []int{10, 20, 30, 40}
for i, num := range nums {
	fmt.Println(i, num)
}
//map
for key, value := range m2 {
	fmt.Println(key, value)
}
```

## 函数

### 参数和返回值

```go
func funcName(param1 Type1, param2 Type2, ...) (return1 Type3, ...) {
    // body
}
func add(num1 int, num2 int) int {
	return num1 + num2
}
```

### 错误处理

```go
import (
	"errors"
	"fmt"
)

func hello(name string) error {
	if len(name) == 0 {
		return errors.New("error: name is null")
	}
	fmt.Println("Hello,", name)
	return nil
}

func main() {
	if err := hello(""); err != nil {
		fmt.Println(err)
	}
}
// error: name is null
```

数组越界，这种错误可能会导致程序非正常退出，在 Go 语言中称之为 panic

```go
func get(index int) (ret int) {
	defer func() {
		if r := recover(); r != nil {
			fmt.Println("Some error happened!", r)
			ret = -1
		}
	}()
	arr := [3]int{2, 3, 4}
	return arr[index]
}

func main() {
	fmt.Println(get(5))
	fmt.Println("finished")
}
```

## 结构体

### 结构体和方法

```go
type Student struct {
	name string
	age  int
}

func (stu *Student) hello(person string) string {
	return fmt.Sprintf("hello %s, I am %s", person, stu.name)
}

func main() {
	stu := &Student{
		name: "Tom",
	}
	msg := stu.hello("Jack")
	fmt.Println(msg) // hello Jack, I am Tom
}
```

- 使用 `Student{field: value, ...}`的形式创建 Student 的实例，字段不需要每个都赋值，没有显性赋值的变量将被赋予默认值，例如 age 将被赋予默认值 0。
- 实现方法与实现函数的区别在于，`func` 和函数名`hello` 之间，加上该方法对应的实例名 `stu` 及其类型 `*Student`，可以通过实例名访问该实例的字段`name`和其他方法了
- 调用方法通过 `实例名.方法名(参数)` 的方式

### 接口

定义一个接口 `Person`和对应的方法 `getName()`

```go
type Person interface {
	getName() string
}

type Student struct {
	name string
	age  int
}

func (stu *Student) getName() string {
	return stu.name
}

func main() {
	var p Person = &Student{
		name: "Tom",
		age:  18,
	}

	fmt.Println(p.getName()) // Tom
}
```

举例

```go
//这个函数接受一个 Value 类型的参数，并调用它的 Len() 方法来打印长度。由于 MyString 和 MySlice 都实现了 Value 接口，它们都可以作为参数传递给 printLength。
func printLength(v Value) {
    fmt.Println(v.Len())
}
func main() {
    str := MyString("Hello, World!")
    slice := MySlice{1, 2, 3, 4, 5}

    printLength(str)   // 输出 13
    printLength(slice) // 输出 5
}
```

Go 语言中，并不需要显式地声明实现了哪一个接口，只需要直接实现该接口对应的方法即可

实例可以强制类型转换为接口，接口也可以强制类型转换为实例

```go
func main() {
	var p Person = &Student{
		name: "Tom",
		age:  18,
	}

	stu := p.(*Student) // 接口转为实例
	fmt.Println(stu.getAge())
}
```

### 空接口

如果定义了一个没有任何方法的空接口，那么这个接口可以表示任意类型

```go
func main() {
	m := make(map[string]interface{})
	m["name"] = "Tom"
	m["age"] = 18
	m["scores"] = [3]int{98, 99, 85}
	fmt.Println(m) // map[age:18 name:Tom scores:[98 99 85]]
}
```

## 并发编程

### sync

Go 语言提供了 sync 和 channel 两种方式支持协程(goroutine)的并发

```go
import (
	"fmt"
	"sync"
	"time"
)

var wg sync.WaitGroup

func download(url string) {
	fmt.Println("start to download", url)
	time.Sleep(time.Second) // 模拟耗时操作
	wg.Done()
}

func main() {
	for i := 0; i < 3; i++ {
		wg.Add(1)
		go download("a.com/" + string(i+'0'))
	}
	wg.Wait()
	fmt.Println("Done!")
}
```

wg.Add(1)：为 wg 添加一个计数，wg.Done()，减去一个计数

go download()：启动新的协程并发执行 download 函数

wg.Wait()：等待所有的协程执行结束

串行需要 3s 的下载操作，并发后，只需要 1s

### channel

```go
var ch = make(chan string, 10) // 缓冲信道允许发送方发送数据到信道，而不需要等待接收方读取数据，只有当缓冲区满时发送方才会被阻塞

func download(url string) {
	fmt.Println("start to download", url)
	time.Sleep(time.Second)
	ch <- url // 将 url 发送给信道
}

func main() {
	for i := 0; i < 3; i++ {
		go download("a.com/" + string(i+'0'))//for 循环启动了3个并发的 download() 协程
	}
	for i := 0; i < 3; i++ {
		msg := <-ch // 等待信道返回消息。
		fmt.Println("finish", msg)
	}
	fmt.Println("Done!")
}
```

## 单元测试

假设我们希望测试 package main 下 `calc.go` 中的函数，要只需要新建 `calc_test.go` 文件

```go
package main

import "testing"

func TestAdd(t *testing.T) {
	if ans := add(1, 2); ans != 3 {
		t.Error("add(1, 2) should be equal to 3")
	}
}
```

## 包和模块

一般来说，一个文件夹可以作为 package，同一个 package 内部变量、类型、方法等定义可以相互看到

```go
// main.go
package main

import "fmt"

func main() {
	fmt.Println(add(3, 5)) // 8
}
```

Go 语言也有 Public 和 Private 的概念，粒度是包。如果类型/接口/方法/函数/字段的首字母大写，则是 Public 

的，对其他 package 可见，如果首字母小写，则是 Private 的，对其他 package 不可见

## model

## container里面有哪些容器

**`container/list`**：提供双向链表的实现，适用于需要频繁插入、删除操作的场景。

**`container/ring`**：提供环形链表的实现，适用于需要循环缓冲区或定期访问的场景。

**`container/heap`**：提供堆的实现，适用于需要快速获取最小（或最大）元素的场景。
