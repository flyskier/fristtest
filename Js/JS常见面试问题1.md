面试遇到的JS问题
========

**1.什么闭包,闭包有什么用，闭包的缺点**

* 指有权访问另一个函数作用域中的变量的函数（内部函数总是可以访问其所在的外部函数中声明的参数和变量，即使在其外部函数被返回（寿命终结）了之后）

* 函数被调用时

      执行环境（execution context）  
      作用域链  
      全局变量对象   
      使用arguments和其他命名参数的值来初始化函数的活动对象（activation object）

* 闭包作用域链通常包括三个部分：

      闭包自己的作用域
      包含函数作用域
      全局作用域

* 闭包常见用途：
      
      1.使用闭包可以在js中模仿块级作用域
      
      2.在对象中创建私有变量、特权变量、储存变量等
      私有变量的实现⽅法很多，有靠约定的（变量名前加_）,有靠Proxy代理的，也有靠Symbol这 种新数据类型的 
      但是真正⼴泛流⾏的其实是使⽤闭包
      function Person(){ 
            var name = 'cxk'; 
            this.getName = function(){ 
                  return name; 
            }
            this.setName = function(value){
                  name = value; 
            } 
      }
      const cxk = new Person() 
      console.log(cxk.getName()) //cxk 
      cxk.setName('jntm') 
      console.log(cxk.getName()) //jntm 
      console.log(name) //name is not defined
      
      
* 闭包的缺点
    
      不必要的闭包只会徒增内存消耗，甚至导致内存泄漏
      闭包只能取得包含函数中的任意变量的最后一个值
      
 
**2.垃圾回收/收集**

 *  原理：找出不再继续使用的变量，然后释放其占用的内存，垃圾收集器会按照固定的时间间隔周期性的执行这一操作
 
 *  垃圾收集策略：
 
    *******1.标记-清除算法*******

         （1）垃圾回收机制维护一系列的根节点，例如window，globle对象等，这些根节点所占用的内存不会被回收；
         （2）从根节点出发，递归的检查子节点，根节点和所有子节点都标记为引用状态，内存不会被回收；
         （3）所有没有标记的内存块，视为垃圾内存，自动回收，由系统重新分配；

    *******2.引用计数*******
       
          容易引起循环引用，改方法IE9以下有问题，不是主流方法

* 内存泄漏：无效引用即无法被程序使用，但又没有被系统回收的内存。

* 几种常见的内存泄漏

  *******(1)全局变量：xxx === window.xxx*******

         解决办法： var  let  const ； 如果不得不使用全局变量，引用之后，手动设置xxx＝null

  *******(2)setInterval中引用的变量和对象：未清除定时器，这些变量和对象一直存在内存中*******

         解决办法：clearInterval（）清除定时器

  *******(3)dom事件没有移除： dom节点被移除但事件依然存在内存中*******
        
         解决办法：removeEventListener
                 
  *******(4)循环引用：*******
     
        var a=new Object;
        var b=new Object;
        a.r=b;
        b.r=a;
        这种情况下，老的计数算法（IE6 IE7）会存在内存泄漏，标记清除算法不会内存泄露！
      
  *******(5)dom移除：******* 
  
        var select = document.querySelector;
        var treeRef = select('#tree');
        var leafRef = select('#leaf');   //在COM树中leafRef是treeFre的一个子结点
        select('body').removeChild(treeRef);//#tree不能被回收入，因为treeRef还在
          
  *******(6) 闭包*******
 
