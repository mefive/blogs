第2条 浮点运算
Javascript所有数字均为64位double型。
小数算不准。比如：

    0.1 + 0.2 == 0.3 //false 0.30000000000000004
    (0.1 + 0.2) + 0.3 == 0.1 + (0.2 + 0.3) //false 前者等于0.6000000000000001
   
故一切小数均应该转化为整数进行运算，然后再转为小数。

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

     var v = "global";
     function() {
          var v = "local";
          
          eval("v"); //local
          (0, src)("v”); //global
     }
第24条 使用变量保存arguments的引用

     function values() {
          var i = 0, n = arguments.length;
          return {
               hasNext: function(){
                    return i < n;
               },
               next: function(){
                    if(i >= n) {
                         throw new Error(“end of iteration”);
                    }
                    return arguments[i++]; //此时的arguments是next的
               }
          };
     }

     var it = values(1, 4, 1, 4, 2, 1, 3, 5, 6);
     it.next(); //undefined 参数为空
第64条 对异步循环使用递归
     保证执行次序 顺序执行 限制条件是只能调用相同的处理函数

     //同步的版本 阻塞依次执行downloadSync
     function downloadOneSync(urls) {
          for(var i = 0, n < urls.length; i < n; i++) {
               try {
                    return downloadSync(url[i]);
               } catch(e) { }
          }
          throw new Error(“all downloads failed”);
     }
     
     //异步版本 非阻塞 依次执行
     function downloadOneAsync(urls, onsuccess, onfailure) {
          var n = urls.length;

          function tryNextURL(i) {
               if(i >= n) {
                    return;
               }
               downloadAsync(urls[i]. onsuccess, function(){
                    tryNextURL(i + 1);
               });
          };

          tryNext(0); //从0开始计数
     }
     
第66条 使用计数器执行并行异步操作
     限制条件是，并行操作间不能有依赖，无法保证执行次序

     function downloadAllAsync(urls, onsuccess, onerror){
          var pending = urls.length, //剩余完毕的数量
               result = [];

          if(length === 0) {
               setTimeout(onsuccess.bind(null, result), 0); //异步立即执行
               return;
          }

          urls.forEach(function(urls, i) {
               downloadAsync(url, function(text) {
                    //成功的回调
                    if(result) {
                         result[i] = text; //保存结果到对应的index上
                         pending--;
                         if(pending === 0) {
                              onsuccess(result); //没有剩余任务了 即都成功了
                         }
                    }
               }, function(error) {
                    if(result) {
                         result = null;
                         onerror(error);
                    }
               })
          });
     }


