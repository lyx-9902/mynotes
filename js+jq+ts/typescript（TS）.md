# 简介  typescript

*TypeScript* 是 JavaScript 的一个超集,支持 ECMAScript 6 标准(ES6 教程)。 *TypeScript* 由微软开发的自由和开源的编程语言。它在开发大型应用的时候可以让产品更加可控。

TypeScript是[微软](https://baike.baidu.com/item/微软/124767)开发的一个开源的[编程语言](https://baike.baidu.com/item/编程语言/9845131)，通过在[JavaScript](https://baike.baidu.com/item/JavaScript/321142)的基础上添加静态类型定义构建而成。TypeScript通过TypeScript[编译器](https://baike.baidu.com/item/编译器/8853067)或Babel转译为JavaScript代码，可运行在任何[浏览器](https://baike.baidu.com/item/浏览器/213911)，任何[操作系统](https://baike.baidu.com/item/操作系统/192)



# 1. 安装

npm方式安装ty插件    全局安装

```
npm install -g typescript
```

查看版本号：  

```
tsc -v    // Version 4.2.4
```

# 2 编译

 文件特征：

index.ts 

浏览器只识别 javascirpt ,所以需要编译。

手动编译  tsc index.ts     会在当前目录中生成一个index.js文件

自动编译：

```
js文件坐在目录，执行命令。生成 tsconfig.json文件
tsc --init

配置文件中，解开注释 ，解析输出文件
"outDir": "./js",   
```

vscode 编辑器    终端 ->  运行任务  ->  点击  监控 tsconfig.json

 效果是： vscode 自动监控该文件， 并执行编译



# 3.  typescript的数据类型

typescript 可以规定数据类型，限制中途变更。

布尔类型  boolean

数字类型  number

字符串类型 string

数组类型 tuple

枚举类型 enum

任意类型  any 

null 和  undefined （null也是一种数据类型）

void类型

never类型

```
let string1:string = "000"
 
string1 = 111  // 报错
```



定义数组：

```
声明数组
 表示: 数字型的数组
 第一种：
let arr:number[] = [1,2,3,'string']  // 报错

let arr:string[] = ['string']  // string类型的数组

第二种
let ar1r:Array<number> = [1,2,3,]  数字型的数组
 
第三种  元祖类型   
指定规定位置的数据类型
let arr2:[string,number,boolean] = ['string',3,false]

```

### 枚举类型

作用： 语义化， 只需记住变量名，自动获取code。标识状态

```
// 枚举枚举
enum Flag {success = 1,error = -1 }

var f:Flag = Flag.success
console.log(f)
枚举的默认赋值

enum Flag {success = 1,error}

var f:Flag = Flag.error
console.log(f) // 2    由于他前面的是1， 后面默认递增

```

### 任意类型案例

```
any 不控制类型，可以随便赋值。 使用场景是： 获取dom, 进行js 样式修改

var num:any = 123;
num ="str" ;
num =true;

```

其他数据类型

undefined 场景; 

定义未赋值 undefined 

```
01.
let num:number;
console.log(num) //undefined
02.
let num:undefined;
console.log(num)  //undefined
这两种情况都是undefined

```

声明两种数据类型

```
let num:undefined|number;
num =123
console.log(num)  //123
案例：
             num 可以是number string
let num:string|number;
num =111
console.log(num)  
```

### void 类型

typescirpt中表示没有任何类型，一般用于定义方法的时候，方法没有返回值

```

function run():void {
    console.log(0)
}
run() //0


显示返回值： number, 如果不是就报错
function run():number {
   return 123;
}
run() 

```

never类型

是其他类型 （包括null 和 undefined）的子类型，发表从不会出现的值。

这意味着声明never的变量只能被never类型索赋值。

# 4  ts中定义函数

### 4.1声明法

```
function run():string{
    return "111"
}
```

### 4.2匿名函数

```

let  run = function():string{
    return "111"
}
run()
```

###  4.3 定义方法传参

```
指定传参的类型，和返回值的类型 ； 否则就报错
function getinfo(name:string,age:number):string{
  return `${name}`
}
console.log(getinfo("tom",20))

let getinfo = function (name:string,age:number):string{
  return `${name}`
}
console.log(getinfo("tom",20))

// 没有返回值
function run():void{
    console.log("run")
}
run()
```

### 4.4 方法可选参数

es5里面方法的实参和形参可以不一样，但是ts中必须一样，如果不一样就需要配置可选参数 （？表示可以不传）

```js
function getinfo(name:string,age?:number):string{
    if(age){
        return `${name}`
    }else{
        return `${name}---年两保密`
    }
}
alert(getinfo("tom"))

注意点： 可选参数放到最后面
```

### 4.5  默认参数

```
function getinfo(name:string,age:number=20):string{
    if(age){
        return `${name}`
    }else{
        return `${name}---年两保密`
    }
}
```

### 4.6 剩余参数

```
1.
// function sum(a:number,b:number){
//     return a+b
// }
// alert(sum(1,2))

2.
// es6中的剩余运算符
function sum(...result:number[]):number{

 var t = 0;
 for(var i =0; i<result.length; i++){

     t+= result[i] 
 }
 return t;
}
alert(sum(1,2))
3.
含义是：1赋值给a, 其余的都给result
function sum(a:number, ...result:number[]):number{

 var t = 0;
 for(var i =0; i<result.length; i++){

     t+= result[i] 
 }
 return t;
}
alert(sum(1,2))
```

### 4.7 函数的重载

java中方法的重载指的是两个或者两个以上同名函数，但是他们的参数不同，这是就会出现函数重载的情况

ts中的重载，通过为同一个函数提供多个函数类型定义来实现多种功能的目的。

```

function css(a){}

function css(a,b){}

es5中 出现这种情况，下面的会替换上面的方法。而ts中，支持这种写法


function getinfo(name:string):string;
function getinfo(age:number):string;
function getinfo(str:any):any{
if(typeof str ==="string"){
    return "我叫"+str
}else{
    return "年龄是"+str
}
}

alert(getinfo(20))
```

第二种：

```
function getinfo(name:string):string;
function getinfo(name:string,age:number):string;

function getinfo(name:any , age?any):any{
if(age){
    return "年龄是"+age
 
}else{
     return "我叫"+name
}
}
alert(getinfo("tom",20))
```

8 箭头函数 es6

```
setTimeout(()=>{
    alert(0)
    },500)
```

# 5 typescript 中的类

### 5.1   es5中的类

```
    // 构造函数和原型链上增加方法 
    function Person() {
        this.name = "tom";
        this.run = function () {
            alert(this.name + '在运动')
        }
    }

*1.   var n = new Person();
    // alert(n.name)
    // n.run() // 执行方法

*2.  // 原型链上增加方法 
    Person.prototype.sex = "男";
    Person.prototype.work = function(){
        alert(this.name +"在工作中")
    }

var p = new Person();
p.work() // 调用原型链上的方法

 *3. 构造函数上的静态方法
Person.getinfo = function(){
    alert('我是静态方法')
}

Person.getinfo(); // 执行静态方法
******
区别： 原型链上的方法 ，每个实例都可以使用， 构造函数不会。
//4.  web类  集成Person类  原型链 +对象冒充的组合集成模式

// 4.1 第一种测试
// function Web(){
//     Person.call(this) // 对象冒充痴线继承
// }

// var w = new Web();
// w.run(); // 对象冒充可以继承构造函数里面的属性和方法
// w.work(); //w.work is not a function   对象冒充 不能继承原型链上面的属性和方法
// 4.2 第二种测试

function Web(){}

Web.prototype = new Person; //将Person实例 放到Web原型链上
var w = new Web();
w.run(); // 可以执行
w.work();  // 可以执行
//  原型链实现的继承：可以继承构造函数里面的属性和方法，也可以继承原型链上面的属性和方法。
4.3
原型链直接赋值，也是可以
function Web(name){
    Person.call(this,name) // 对象冒充继承，也可以传参
}

var  w = new Web("tom");
w.run()
```

### 5.2   ts中的类

### 01.定义类 

（类中：属性 和方法 ）

```
class Person{
     name:string; //属性 前面省略了public关键词
     constructor(n:string){ // 构造函数 实例化类的时候触发的方法
       this.name = n;
     }
  run():void{
      alert(this.name)
  }
}
var p = new Person("tom");
p.run()
```

 通过方法，修改属性，并执行以下方法

```
class Person{

     name:string; //属性 前面省略了public关键词

     constructor(n:string){ // 构造函数 实例化类的时候触发的方法

       this.name = n;
     }

     getName():string{
         return this.name
     }
     setName(name:string):void{
         this.name = name;
     }
}
var p = new Person("tom");

  p.setName("张三")
console.log(p.getName())
```

### 02 ts 中实现继承 

 extends ，super

 继承的目的：就是可以使用父类的 属性和方法，同时，也可以创建自己的属性和方法

 注意点：当父类和自己的方法重名的时候，  自己的方法优先级最高。 先从自己的方法中查找，没有的话再去父类中查找。

```
class Person{

     name:string; //属性 前面省略了public关键词

     constructor(n:string){ // 构造函数 实例化类的时候触发的方法

       this.name = n;
     }

     run():string{
         return this.name+"在运动"
     }
}
class Web extends Person{  // extends 关键字 表示继承
    constructor(name:string){
        super(name)  // super 初始化父类的构造函数
    }
       work(){
        alert(this.name+"在工作")
    }
}
var w = new Web("李四");
alert(w.run())  // 使用父类的方法
alert(w.run())  // 使用自己的方法
```

###  3 ts中类里面的修饰符

类里面的修饰符 ts里面定义属性的时候给我们提供了三种修饰符

public 共有 在类里面 子类 类外面都可以访问

protected 保护类型 在类里面，子类里面可以访问 在类外部没法访问

private 私有 在类里面可以访问， 子类 ，类外部不能访问

   注意：子类指的是 继承父类的类。

属性如果不加修饰符 默认 public

**  如何使用修饰符

​      public name:string; //属性  公有

```
class Person{
    public name:string; //属性  公有
     constructor(n:string ){ 
       this.name = n;  //  01 自己使用
     }
     run():string{
         return this.name+"在运动"
     }
}
class Web extends Person{  
    constructor(name:string){
        super(name)  
    }
    work(){
        alert(this.name+"在工作")  //  02 自子类使用
    }
}
var w = new Web("李四");
alert(w.name)   //  03 类外部使用



```

### 4 ts 静态属性和方法

es5中的

什么是静态方法 ， 实例方法。 以及方法的调用

静态属性和实例的属性   和使用

```

function Person(){
    this.run1 = function(){}//实例方法
}

Person.run2 = function(){ } //静态方法

//实例方法的调用
var p = new Person();
   p.run1()

//静态方法的调用
Person.run2()
```

经典案例： jquery

```
// 实战检测
// jQuery 的封装逻辑
   function $(element){
     return new Base(element){ }
   }
    $.get = function(){}

     function Base(element){
            this.element = "获取节点";
         this.CSS = function(arr,value){
        this.element.style.arr = value;
      }      
   }
 
// 使用：
$("#box").css('color','red')  // 使用实例方法
$.get("url",data) // 使用静态方法
```

### ts定义静态方法和实例方法

```
class Person{
    public name:string;
    public age:number =20;  //静态属性
    static sex = "男";

     constructor(n:string ){ 
       this.name = n; 
     }

     run(){     //实例方法
        alert(`${this.name}在运动`)
     }
     work(){
        alert(`${this.name}在工作`)  
     }
     static print(){
         alert(`获取静态属性上的性别 ${Person.sex}`)
     }
}

 // 执行静态方法
Person.print()
 // 执行实例方法
 var p = new Person("张三");
   p.work()

//    总结： ts中的 静态方法和实例方法 以关键字 static 表示；并且各自使用各自的属性
```

### 5 ts抽象类 继承 多态

 es5中多态定义：

父类定义一个方法不去实现，让继承他的子类去实现，每一个子类有不同的表现；

多态属于继承

```

class Animal{
    name:string;
    constructor(name:string){
        this.name =name;
    }
    eat(){ // 具体吃什么
           console.log("吃的方法")
    }
}
    class Dog extends Animal{
        constructor(name:string){
            super(name)
        }
            eat(){
                return this.name+"吃狗粮"
            }
    }

    class Cat extends Animal{
        constructor(name:string){
            super(name)
        }
            eat(){
                return this.name+"吃猫粮"
            }
    }
```

ts的多态   就是 抽象类的相关规则

```
//  ts中的抽象类： 他是提其他类继承的基类，不能直接被实例化、
//  用abstract关键字定义抽象类和抽象方法，抽象类中的抽象方法不包含具体实现并且必须在子类中实现
// abstract 抽象方法只能放在抽象类中
// 抽象类和抽象方法用来定义标准， 标准Animal这个类，要求他的子类必须包含eat方法

abstract class Animal {
    public name:string;
    constructor(name:string) {
        this.name = name;
    }
    abstract eat():any;//抽象类中的抽象方法不包含具体实现
}

// var a = new Animal(); // 报错，提示不能实例化抽象类
class Dog extends Animal {
    constructor(name:nay) {
        super(name)
    }
    run(){};
    eat(){  // 子类必须包含父类 的抽象方法
        console.log(this.name + "吃狗粮")
    }
}
var d = new Dog("小狗");
d.eat() // 可以执行

// 总结： 抽象类就是规定类， 子类继承时，要按照规定定义自己的方法
```

# 6 ts 接口

属性接口

可索引接口

类类型接口

接口扩展

接口的作用： 在面向对象的编程中，接口是一种规范的定义，它定义了行为和动作的规范，在程序设计里面，接口起到了一种限制和规范的作用。接口定义了某一批类所需要遵守的规范，接口不关心这些类的内部状态数据，也不关心这些类里方法的实现细节，它只规定这批类里必须提供某些方法，提供这些方法的类就可以满足实际需要、ts中的接口类似于java,同时还增加了更灵活的接口类型，包括属性，函数，可索引和类等。



# 分割线----------

# 原始类型

js有五种基本类型 string、number、boolean、null、undefined，这几种类型typescript都赋予了对应的类型限定，如下：

1. 布尔值

   ```cpp
    var  bool: boolean = false     
   ```

   注意`利用Boolean创造的对象不是布尔值:

   

   ```tsx
   let boolObject: boolean = new Boolean(1) //会报错
   ```

   new Boolean创造的是一个对象并不是布尔值，

   直接调用Boolean倒是可以

   ```tsx
    let bool: boolean = Boolean(1) 
   ```

2. 字符串

   

   ```tsx
    str: string = 'hellow'
   // 模板字符串
   let sentence: string = `Hello, my name is ${myName}.
   I'll be ${myAge + 1} years old next month.`;      
   ```

   编译结果：

   

   ```go
     var myName = 'Tom';
   var myAge = 25;
   // 模板字符串
   var sentence = "Hello, my name is " + myName + ".\nI'll be " + (myAge + 1) + " years old next month.";      ```
   ```

3. 数值

   

   ```tsx
   let decLiteral: number = 6;
   let hexLiteral: number = 0xf00d;
   // ES6 中的二进制表示法
   let binaryLiteral: number = 0b1010;
   // ES6 中的八进制表示法
   let octalLiteral: number = 0o744;
   let notANumber: number = NaN;
   let infinityNumber: number = Infinity;     
   ```

   编译结果：

   

   ```jsx
      var decLiteral = 6;
   var hexLiteral = 0xf00d;
   // ES6 中的二进制表示法
   var binaryLiteral = 10;
   // ES6 中的八进制表示法
   var octalLiteral = 484;
   var notANumber = NaN;
   var infinityNumber = Infinity;      
   ```

   其中 `0b1010` 和 `0o744` 是 [ES6 中的二进制和八进制表示法](https://links.jianshu.com/go?to=http%3A%2F%2Fes6.ruanyifeng.com%2F%23docs%2Fnumber%23%E4%BA%8C%E8%BF%9B%E5%88%B6%E5%92%8C%E5%85%AB%E8%BF%9B%E5%88%B6%E8%A1%A8%E7%A4%BA%E6%B3%95)，它们会被编译为十进制数字。

4. null和undefined

   null和undefined在typescript中分别是两个独立的类型限定：

   

   ```jsx
     let u: undefined = undefined;
     let n: null = null;     
   ```

   undefined限定的变量只能赋值undefined，null也一样。

5. 空值void
    void限定的变量只能赋值null或者undefined：

   

   ```csharp
    let noContent: void = null;
   ```

   与null和undefined限定不同的是，null和undefined是所有类型的子类型：

   

   ```tsx
     let num: number = undefined; //这样没有问题
   // 这样也不会报错
   let u: undefined;
   let num: number = u;
   ```

   而void类型的变量不能互相随意传递：

   

   ```tsx
     let noContent: void;
     let num: number = noContent; // 报错
   ```

6. 任意类型 (any)

   被指定为任意类型的变量可以被赋值任何类型，也能被调用任何属性方法，都不会报错:

   

   ```tsx
   let myFavoriteNumber: string = 'seven';
   myFavoriteNumber = 7;
   
   let anyThing: any = 'Tom';
   anyThing.setName('Jerry');
   anyThing.setName('Jerry').sayHello();
   anyThing.myName.setFirstName('Cat');
   ```

   注意：`没有指定类型的变量，默认就是any类型`。

## 类型推论

当变量被赋值的时候没有被指定类型限定，会根据变量类型默认设置类型限定：



```csharp
let myFavoriteNumber = 'seven';
myFavoriteNumber = 7;

// 等价于下边
let myFavoriteNumber: string = 'seven';
myFavoriteNumber = 7;
```

## 联合类型

表示取值为多种类型中的一个



```tsx
let myFavoriteNumber: string | number;
myFavoriteNumber = 'seven';
myFavoriteNumber = 7;
// 只能赋值string或者number
myFavoriteNumber = true // 会报错
```

### 访问联合类型的属性和方法

联合类型的变量只能访问类型共有的属性和方法



```tsx
function getLength(something: string | number): number {
   return something.length; // 会报错，字符串不含有length属性
 //想解决报错可以使用类型断言
 return <string>something.length // 这样就不会报错
}
// 联合类型当赋值为一个类型会推断赋值为那个类型
myFavoriteNumber = 'ss' // 变量被设定为字符串
myFavoriteNumber.slice(0) // ok
myFavoriteNumber = 5 // 变量被推断为number类型
myFavoriteNumber.slice(0) // 会报错
```

## 接口

`接口`是面向对象中的概念，表示行为的抽象，具体如何行动通过类实现，在typescript中本人觉得接口主要是起到对编码中的一种约束，可以减少很多错误，并且配合很多ide（比如webstorm）代码提示可以提高编码效率。

### 简单例子



```tsx
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
    age: 25
}; // ok
let lilei: Person = {
      name: 'Tom',
    age: 25,
  sexy: 'name'
} // 错误 sexy属性并没有定义
```

### 可选属性

上边例子中定义的Person接口限定的变量，必须同时设置name和age两个属性，不然会报错：



```tsx
interface Person {
    name: string;
    age: number;
}

let tom: Person = {
    name: 'Tom',
}; // error 缺少 age属性
```

如果要解决这个，就需要设置可选属性，在变量前边加上`？`：



```tsx
interface Person {
   name: string;
   age?: number;
}

let tom: Person = {
   name: 'Tom'
};//ok
```

### 任意属性

有时候我们希望一个接口准许有任意属性，可以使用如下方式：



```tsx
interface Person {
   name: string;
   age?: number;
   [propName: string]: any;
}

let tom: Person = {
   name: 'Tom',
   gender: 'male'
}; // ok
```

使用 `[propName: string]` 定义了任意属性取 `string` 类型的值。

需要注意的是，**一旦定义了任意属性，那么确定属性和可选属性的类型都必须是它的类型的子集**：



```tsx
interface Person {
  name: string;
  age?: number;
  [propName: string]: string;
}

let tom: Person = {
  name: 'Tom',
  age: 25,
  gender: 'male'
};
```

上边例子中`[propName: string]: string;`将整个接口设置；属性名为string类型，属性值为string类型，age值为number不符合这个类型，所以报错。

### 只读属性

有时候我们希望对象中的一些字段只能在创建的时候被赋值，那么可以用 `readonly` 定义只读属性，只读属性有两个约束：

1. 对象创建时候要赋值
2. 赋值后不能再重新修改属性值了

例子：



```tsx
interface Person {
    readonly id: number;
    name: string;
    age?: number;
    [propName: string]: any;
}

let tom: Person = {
    name: 'Tom',
    gender: 'male'
}; // 报错 没有给id赋值

tom.id = 89757; // id是只读，不能修改
```

## 数组类型

### 数组类型定义方式

#### 类型 + 方括号



```tsx
let fibonacci: number[] = [1, 1, 2, 3, 5];
fibonacci.push(true) // 报错  不是number类型
```

#### 数组范型



```tsx
let fibonacci: Array<number> = [1, 1, 2, 3, 5];
```

#### 接口表示



```tsx
interface NumberArray {
    [index: number]: number;
}
let fibonacci: NumberArray = [1, 1, 2, 3, 5];
```

## 函数类型

### 函数声明



```tsx
function sum(x: number, y: number): number {
    return x + y;
}

// 表达式声明方式
let mySum = function (x: number, y: number): number {
    return x + y;
};
```

Typescript添加了对函数变量和返回值类型的限定

### 接口定义函数类型



```tsx
interface SearchFunc {
    (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string, subString: string) {
    return source.search(subString) !== -1;
}
```

### 可选参数

函数有时候会定义一些是必须传递的参数，函数的可选参数定义和接口中对象的可选参数定义方式一样，都是使用`？`，如下：



```tsx
function buildName(firstName: string, lastName?: string) {
    if (lastName) {
        return firstName + ' ' + lastName;
    } else {
        return firstName;
    }
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom')
```

注意：可选参数必须接在必需参数后面。换句话说，**可选参数后面不允许再出现必须参数了**：



```tsx
function buildName(firstName?: string, lastName: string) {
    if (firstName) {
        return firstName + ' ' + lastName;
    } else {
        return lastName;
    }
} // 报错
```

### 参数默认值

在 ES6 中，我们允许给函数的参数添加默认值，**TypeScript 会将添加了默认值的参数识别为可选参数**：



```csharp
function buildName(firstName: string, lastName: string = 'Cat') {
    return firstName + ' ' + lastName;
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom');
```

此时就不受可选参数必须接在必须参数后面的限制了：



```jsx
function buildName(firstName: string = 'Tom', lastName: string) {
    return firstName + ' ' + lastName;
}
let tomcat = buildName('Tom', 'Cat');
let cat = buildName(undefined, 'Cat');
```

### 剩余参数

ES6 中，可以使用 `...rest` 的方式获取函数中的剩余参数（rest 参数）：



```php
function push(array, ...items) {
    items.forEach(function(item) {
        array.push(item);
    });
}

let a = [];
push(a, 1, 2, 3);
```

## 类型断言

类型断言（Type Assertion）可以用来手动指定一个值的类型。

### 方式

> <类型>值

或

> 值 as 类型

在 tsx 语法（React 的 jsx 语法的 ts 版）中必须用后一种。

### 使用场景

之前有个例子当函数变量使用联合类型，如果我们在函数体中需要特定类型的方法，就需要使用类型断言，不然编译的时候就会报错：



```tsx
function getLength(something: string | number): number {
    if ((<string>something).length) {
        return (<string>something).length; //不加类型断言就会报错
    } else {
        return something.toString().length;
    }
}
```

**注意**，类型断言不是类型转换，断言一个联合类型不存在的类型会报错：



```tsx
function toBoolean(something: string | number): boolean {
    return <boolean>something; // 报错， 布尔类型不能赋值给something
}
```

## 字符串字面量类型

字符串字面量类型用来约束取值只能是某几个字符串中的一个



```jsx
type EventNames = 'click' | 'scroll' | 'mousemove';
function handleEvent(ele: Element, event: EventNames) {
    // do something
}

handleEvent(document.getElementById('hello'), 'scroll');  // 没问题
handleEvent(document.getElementById('world'), 'dbclick'); // 报错，event 不能为 'dbclick'
```

## 元组

元组可以理解为存储不同类型值的数组



```tsx
let tulpe: [string, number] = ['tom', 25];
//或者
let tulpe: [string, number];
tulpe[0] = 'tom';
tulpe[1] = 25;

tulpe[0].slice(1);
tulpe[1].toFixed(2);

//也可以只赋值其中一项
let tulpe: [string, number];
tulpe[0] = 'tom';

tulpe.push(true);// 报错 赋值类型不存在申明类型中
```

元组使用上需要特别注意的是：

元组初始化的时候必须赋值元组声明的所有类型变量：



```tsx
let tulpe: [string, number] = ['tom']; // 报错
// 或者
let tulpe: [string,number];
tulpe = ['tome'] // 报错
```

## 枚举

枚举（Enum）类型用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等。

### 典型例子



```jsx
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};
console.log(Days["Sun"] === 0); // true
console.log(Days["Mon"] === 1); // true
console.log(Days["Tue"] === 2); // true
console.log(Days["Sat"] === 6); // true

console.log(Days[0] === "Sun"); // true
console.log(Days[1] === "Mon"); // true
console.log(Days[2] === "Tue"); // true
console.log(Days[6] === "Sat"); // true

//编译后的样子
var Days;
(function (Days) {
   Days[Days["Sun"] = 0] = "Sun";
   Days[Days["Mon"] = 1] = "Mon";
   Days[Days["Tue"] = 2] = "Tue";
   Days[Days["Wed"] = 3] = "Wed";
   Days[Days["Thu"] = 4] = "Thu";
   Days[Days["Fri"] = 5] = "Fri";
   Days[Days["Sat"] = 6] = "Sat";
})(Days || (Days = {}));
```

### 手动复制

我们也可以给枚举项手动赋值：



```cpp
enum Days {Sun = 7, Mon = 1, Tue, Wed, Thu, Fri, Sat};

console.log(Days["Sun"] === 7); // true
console.log(Days["Mon"] === 1); // true
console.log(Days["Tue"] === 2); // true
console.log(Days["Sat"] === 6); // true
```

未手动赋值的枚举类型变量会自动赋值（在前边变量值逐步累加1）

值得注意的是：**如果未手动赋值的枚举项与手动赋值的重复了，TypeScript 是不会察觉到这一点的**：



```cpp
enum Days {Sun = 3, Mon = 1, Tue, Wed, Thu, Fri, Sat};

console.log(Days["Sun"] === 3); // true
console.log(Days["Wed"] === 3); // true
console.log(Days[3] === "Sun"); // false
console.log(Days[3] === "Wed"); // true
```

### 常数项和计算所得项

枚举项有两种类型：常数项（constant member）和计算所得项（computed member）。

前面我们所举的例子都是常数项，一个典型的计算所得项的例子：



```rust
enum Color {Red, Green, Blue = "blue".length};
```

上面的例子中，`"blue".length` 就是一个计算所得项。

上面的例子不会报错，但是**如果紧接在计算所得项后面的是未手动赋值的项，那么它就会因为无法获得初始值而报错**：



```rust
enum Color {Red = "red".length, Green, Blue};
```

### 常数枚举

常数枚举是使用 `const enum` 定义的枚举类型：



```rust
const enum Directions {
    Up,
    Down,
    Left,
    Right
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
```

常数枚举与普通枚举的区别是，**它会在编译阶段被删除，并且不能包含计算成员**。

上例的编译结果是：



```csharp
var directions = [0 /* Up */, 1 /* Down */, 2 /* Left */, 3 /* Right */];
```

### 外部枚举

外部枚举（Ambient Enums）是使用 `declare enum` 定义的枚举类型：



```rust
declare enum Directions {
   Up,
   Down,
   Left,
   Right
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
```

之前提到过，`declare` 定义的类型只会用于编译时的检查，编译结果中会被删除。

上例的编译结果是：



```csharp
var directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
```

## 类

### typescript中类增加的内容

1. 限定符

   TypeScript 可以使用三种访问修饰符（Access Modifiers），分别是 `public`、`private` 和 `protected`。

   - `public` 修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 `public` 的
   - `private` 修饰的属性或方法是私有的，不能在声明它的类的外部访问
   - `protected` 修饰的属性或方法是受保护的，它和 `private` 类似，区别是它在子类中也是允许被访问的

2. 抽象类



```csharp
     abstract class Animal { // abstract标志类是抽象类
        public name;
        public constructor(name) {
            this.name = name;
        }
        public abstract sayHi();
        }
      let a = new Animal('Jack'); // 报错 抽象类不能实例化
```

抽象类正确的使用方式:



```tsx
       abstract class Animal {
        public name;
        public constructor(name) {
              this.name = name;
        }
        public abstract sayHi();
        }

      class Cat extends Animal {
        public sayHi() { // 实现抽象类中的方法
          console.log(`Meow, My name is ${this.name}`);
        }
    }
    let cat = new Cat('Tom');
```

### 类的类型

类也可以作为一个**类型**来使用



```tsx
    class Animal {
    name: string;
    constructor(name: string) {
        this.name = name;
    }
    sayHi(): string {
      return `My name is ${this.name}`;
    }
    }
    let a: Animal = new Animal('Jack');
    console.log(a.sayHi()); // My name is Jack
```

## 类与接口

实现（implements）是面向对象中的一个重要概念。一般来讲，一个类只能继承自另一个类，有时候不同类之间可以有一些共有的特性，这时候就可以把特性提取成接口（interfaces），用 `implements` 关键字来实现。这个特性大大提高了面向对象的灵活性。

### 类实现接口



```dart
interface Alarm {
   alert();
}

class Door {
}

class SecurityDoor extends Door implements Alarm {
   alert() {
       console.log('SecurityDoor alert');
   }
}

class Car implements Alarm {
   alert() {
       console.log('Car alert');
   }
}
```

### 接口继承接口



```dart
interface Alarm {
   alert();
}

interface LightableAlarm extends Alarm {
   lightOn();
   lightOff();
}
```

### 接口继承类

接口也可以继承类：



```tsx
class Point {
   x: number;
   y: number;
}

interface Point3d extends Point {
   z: number;
}
let point3d: Point3d = {x: 1, y: 2, z: 3};
```

## 泛型

泛型（Generics）是指在定义函数、接口或类的时候，不预先指定具体的类型，而在使用的时候再指定类型的一种特性。

### 典型的例子

首先，我们来实现一个函数 `createArray`，它可以创建一个指定长度的数组，同时将每一项都填充一个默认值：



```tsx
function createArray<T>(length: number, value: T): Array<T> {
  let result: T[] = [];
  for (let i = 0; i < length; i++) {
      result[i] = value;
  }
  return result;
}

createArray<string>(3, 'x'); // ['x', 'x', 'x']
```

上例中，我们在函数名后添加了 `<T>`，其中 `T` 用来指代任意输入的类型，在后面的输入 `value: T` 和输出 `Array<T>` 中即可使用了。

接着在调用的时候，可以指定它具体的类型为 `string`。当然，也可以不手动指定，而让类型推论自动推算出来：

### 多个类型参数

定义泛型的时候，可以一次定义多个类型参数：



```tsx
function swap<T, U>(tuple: [T, U]): [U, T] {
  return [tuple[1], tuple[0]];
}

swap([7, 'seven']); // ['seven', 7]
```

### 泛型约束

在函数内部使用泛型变量的时候，由于事先不知道它是哪种类型，所以不能随意的操作它的属性或方法：



```jsx
function loggingIdentity<T>(arg: T): T {
  console.log(arg.length);
  return arg;
}
```

上例中，泛型 `T` 不一定包含属性 `length`，所以编译的时候报错了。

这时，我们可以对泛型进行约束，只允许这个函数传入那些包含 `length` 属性的变量。这就是泛型约束：



```jsx
nterface Lengthwise {
  length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}
```

多个类型参数之间也可以互相约束：



```bash
function copyFields<T extends U, U>(target: T, source: U): T {
  for (let id in source) {
      target[id] = (<T>source)[id]; // 如果不使用泛型约束，这里会报错
  }
  return target;
}

let x = { a: 1, b: 2, c: 3, d: 4 };

copyFields(x, { b: 10, d: 20 });
```

上例中，我们使用了两个类型参数，其中要求 `T` 继承 `U`，这样就保证了 `U` 上不会出现 `T` 中不存在的字段。

### 泛型接口



```tsx
interface CreateArrayFunc {
  <T>(length: number, value: T): Array<T>;
}

let createArray: CreateArrayFunc;
createArray = function<T>(length: number, value: T): Array<T> {
  let result: T[] = [];
  for (let i = 0; i < length; i++) {
      result[i] = value;
  }
  return result;
}

createArray(3, 'x'); // ['x', 'x', 'x']
```

进一步，我们可以把泛型参数提前到接口名上：



```tsx
interface CreateArrayFunc<T> {
  (length: number, value: T): Array<T>;
}

let createArray: CreateArrayFunc<any>;
createArray = function<T>(length: number, value: T): Array<T> {
  let result: T[] = [];
  for (let i = 0; i < length; i++) {
      result[i] = value;
  }
  return result;
}

createArray(3, 'x'); // ['x', 'x', 'x'] 
```

注意，此时在使用泛型接口的时候，需要定义泛型的类型。

## 泛型类

与泛型接口类似，泛型也可以用于类的类型定义中：



```jsx
class GenericNumber<T> {
  zeroValue: T;
  add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };
```

## 泛型参数的默认类型

在 TypeScript 2.3 以后，我们可以为泛型中的类型参数指定默认类型。当使用泛型时没有在代码中直接指定类型参数，从实际值参数中也无法推测出时，这个默认类型就会起作用。



```csharp
function createArray<T = string>(length: number, value: T): Array<T> {
  let result: T[] = [];
  for (let i = 0; i < length; i++) {
      result[i] = value;
  }
  return result;
}
```

## 声明合并

如果定义了两个相同名字的函数、接口或类，那么它们会合并成一个类型：

### 函数的合并

我们可以使用重载定义多个函数类型：



```tsx
function reverse(x: number): number;
function reverse(x: string): string;
function reverse(x: number | string): number | string {
  if (typeof x === 'number') {
      return Number(x.toString().split('').reverse().join(''));
  } else if (typeof x === 'string') {
      return x.split('').reverse().join('');
  }
}
```

### 接口的合并

接口中的属性在合并时会简单的合并到一个接口中：



```css
interface Alarm {
    price: number;
}
interface Alarm {
    weight: number;
}
```

相当于：



```css
interface Alarm {
  price: number;
  weight: number;
}
```

注意，**合并的属性的类型必须是唯一的**：



```tsx
interface Alarm {
  price: number;
}
interface Alarm {
  price: number;  // 虽然重复了，但是类型都是 `number`，所以不会报错
  weight: number;
}
```



```tsx
interface Alarm {
  price: number;
}
interface Alarm {
  price: string;  // 类型不一致，会报错
  weight: number;
}

// index.ts(5,3): error TS2403: Subsequent variable declarations must have the same type.  Variable 'price' must be of type 'number', but here has type 'string'.
```

接口中方法的合并，与函数的合并一样：



```tsx
interface Alarm {
    price: number;
    alert(s: string): string;
}
interface Alarm {
    weight: number;
    alert(s: string, n: number): string;
}
```

相当于：



```tsx
interface Alarm {
  price: number;
  weight: number;
  alert(s: string): string;
  alert(s: string, n: number): string;
}
```

## 参考资料



作者：大喵爱读书
链接：https://www.jianshu.com/p/ced644f45764
来源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。