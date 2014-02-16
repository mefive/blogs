第4条 原始类型优于封装类型
   
    var str = "abc",
        str1 = "abc";
   
    str === str2; //true
   
    strObj = new String("abc");
    strObj1 = new String("abc");
    strObj === strObj2; //false
   
    str.toUpperCase(); //"ABC" 原始类型可以调用String对象的方法
    str.someProp = 12; //也可以给原始类型变量赋值
    str.someProp; //undefined 但无法访问
   
第5条 避免对混合类型使用“==”
    比较规则是先将对象转化为原始类型(valueOf -> toString)
   
第10条 避免使用with
     with会强行开辟出一片变量作用域，使在其中的变量优先在指定作用域中查找。

     function status(info){
          var widget = new Widget();
          with(widget) {
               setBackground('blue');
               setText('status: ' + info); //这里的info变量会优先在widget对象中查找，但这并非是原意
          }
     } 

第14条 当心命名函数表达式笨拙的作用域

     var constructor = function() {return null;}
     var f = function f() {
          return constructor();
     }
     f(); // {} ES3

     var f = funtion g(){ … } //开辟两个内存空间存储函数

第17条 间接调用eval函数

     (0, eval)(src); 
     //相当于
     var f = eval;
     f(src);  //src可访问的作用域只有全局

     var v = “global”;
     function() {
          var v = “local”;
          
          eval("v"); //local
          (0, src)("v”); //global
     }
     


