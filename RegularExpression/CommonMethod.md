正则对象和正则的写法
========

**新建正则表达式的方法**

* 方法一 字面量的方式

        var re=/a/ ;    ---以斜杠表示开始和结束   
        
* 方法二 RegExp 构造函数

        var re=new RegEx('a'); 
        
* 区别：

  第一种方法在编译时新建正则表达式，第二种方法在运行时新建正则表达式。


**转义字符**

      \s：空格
      \S：非空格    --大写的s
      
      \d：数字
      \D：非数字    --大写的D
      
      \w：字符    (字母，数字，下划线)
      \W：非字符     --大写的W

**i（区分大小写）**

* 正则中默认：是区分大小写的

* 如果不区分大小写的话，在正则的最后加标识 i    

            var res=/a/i;               //找到字符串中的a，A,不区分大小写
            var re=new RegEx('a','i');

            var res=/a/;                //找到字符串中的a, 区分大小写
            var re=new RegEx('a');
            
**g(全局匹配)**

* 正则中默认：正则匹配成功就会结束，不会继续匹配

* 如果想全部查找，在正则的最后加标识 g(全局匹配)  

          var res=/\d/g;               //找到字符串中的所有数字
          var re=new RegEx('\d','g');

         var res=/\d/;                //只会找到字符串中的第一个数字
         var re=new RegEx('\d');
**量词**
* 作用: 匹配不确定的位置 
* '+'至少出现一次 

         var res=/b+/;   找到字符串中的b,bb,bbb,...等中的第一个

         var res=/b+/g;  找到字符串中所有的的b,bb,bbb,...
 
**正则的小括号（）的作用** 

 * 分组操作（优先小括号里面的）
   
 * 匹配子项
        正则的整体叫做（母亲），小括号里面的是就是子项，从左至右小括号包含的依次是第一个子项，第二个子项等等
           
           replace
                var str='2017-6-7';
                var re=/(\d+)(-)/g;
                str.replace(re,function($0,$1,$2){  //参数名随便写，
                //第一个参数：$0  (正则整体/母亲)
                //第二个参数：$1  (第一个子项)
                //第三个参数：$0  (第二个子项) 
                alert($0);     // /(\d+)(-)/g   2017-  6-
                alert($1);     // /(\d+)/g      2017   6
                alert($2);     // /(-)/g         -     -
                });
         
         
            match
                var str='abcd';
                var re=/abc/;
                alert(str.match(re));      //[abc]

                var re1=/(a)(b)(c)/;
                alert(str.match(re1));    //[abc,a,b,c]

                var re2=/(a)(b)(c)/g;
                 alert(str.match(re2));    //[abc]  当match不加g(全局匹配)的时候，才可以获取到子项的集合

**字符类（中括号）**

一组相似的元素，中括号的整体代表一个字符



**|（或）**



**test方法**

* 概念：

  正则去匹配字符串，如果匹配成功就返回真，匹配失败就返回假

* 使用方法：

   正则.test(字符串)

          var str='abc34ds3er';
          var res=/b/;
          alert(res.test(str));    //true

          var res1=/0/;
          alert(res1.test(str));   //false

          var res2=/bd/;
          alert(res2.test(str));   //false
          
 
**search方法**

* 概念：

  正则去匹配字符串，如果匹配成功就返回匹配成功的位置(位置从0开始)，匹配失败就返回-1   

* 使用方法：

   字符串.search（正则）
   
          var str='abc342ds5w';
            var res=/b/;
            alert(str.search(res));    //1

            var res1=/0/;
            alert(str.search(res1));   //-1

            var res=/bc3/;
            alert(str.search(res));   //1  跟Js 中indexOf一致，输出字符串中首字母的位置
            

**match方法**

* 概念：

  正则去匹配字符串，如果匹配成功就返回匹配成功的数组，匹配失败就返回null  

* 使用方法：

   字符串.match（正则）
   
   
**replace方法**

* 概念：

  正则去匹配字符串，如果匹配成功的字符去替换成新的字符

* 使用方法： 

    字符串.replace（正则，新的字符串）或

    字符串.replace（正则，回调函数）
   
replace回调函数的第一个参数：就是匹配成功的字符
   
   
            var str='abc3bb';
            var res=/b/;
            var str1=str.replace(res,'D')
            alert(str1);    //aDc3b

            var str='abc3bb';
            var res=/b/g;
            var str1=str.replace(res,'D')
            alert(str1);    //aDc3DD

            var str='abc3bb';
            var res=/b+/;
            var str1=str.replace(res,'D')
            alert(str1);    //aDc3bb

            var str='abc3bb';
            var res=/b+/g;
            var str1=str.replace(res,'D')
            alert(str1);    //aDc3D
   
   
   
   
   
   
   
 **【参考资料】**
  
  [JavaScript 标准参考教程（alpha）--RegExp对象](http://javascript.ruanyifeng.com/stdlib/regexp.html#toc0)
  
  [妙味官网视频](http://2017.miaov.com/v_show/341)
   
   
   
   
          
