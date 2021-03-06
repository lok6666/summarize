#解构赋值
##es6按照一定的模式，从数组和对象中提取值，对变量进行赋值，被称为解构赋值。
1. 数组，对象的解构赋值。
  1.1. 数组的解构赋值。
  let [x, , y] = [1, 2, 3];
  console.log(x,y);//1 3
  let[,,third]=["2","3","3"];
  console.log(third);//3
  注：1.1.1. 解构不成功，返回underfined。
      var [foo2] = [];
      var [bar2, fee2] = [1];
      console.log(foo2,fee2);//undefined
      1.1.2. 如果等号右边不是数组，一定会报错。
      // let [foo] = 1;
      // let [foo] = false;
      1.1.3. 解构赋值中的默认值。
      var [foo3 = true] = [];//foo3 为 true
      [x3, y3 = 'b'] = ['a']; // x3='a', y3='b'
      [x4, y4 = 'b'] = ['a',undefined]; // x4='a'y4='b'
      1.1.4. ES6内部使用严格相等运算符（===），判断一个位置是否有值。
             所以，如果一个数组成员不严格等于undefined，默认值是不会生效的。
              var [x5 = 1] = [undefined];//x5 为 1
              var [x6 = 1] = [null];//x6 为 null
      1.1.5. 默认值可以引用解构赋值的其他变量，但是该变量必须已经声明。
            let [m1 = 1, n1 = m1] = []; // m1=1; n1=1
            let [m2 = 1, n2 = m2] = [2]; // m2=2; n2=2
            let [m3 = 1, n3 = m3] = [1, 2]; // m3=1; n3=2
            let [m4 = n4, n4 = 1] = []; // ReferenceError
            console.log(m1,n1,m2,n2,m3,n3);
      1.1.6. let创建引用对象。
            let a = [];
            let b=[2,3,4];
            [a[0],a[1],a[2]] = b;
            console.log(a == b);//false

            let a = [];
            let b=[2,3,4];
            a = b;
            console.log(a == b);//true
  1.2. 对象的解构赋值。
      1.2.1. 对象解构基本形式。
            let{a}={a:"1",b:"2",c:"3"};
            console.log(a);
      1.2.2. 左侧为键值对时,注意键值对赋值时的对应关系
            var { foo4: baz4 } = { foo4: 'aaa', bar4: 'bbb' };
            console.log(baz4);// "aaa"
      1.2.3. 解构赋值匹配的是，赋的其实是值。
            let obj1 = { first: 'hello', last: 'world' };
            let { first: f, last: l } = obj1;
            console.log(f,l);//注意和下边写法的区别
            let { first, last } = obj1;
            console.log(first,last)
      1.2.4. 对象的解构赋值的内部机制，是先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。 
      var { foo6: baz6 } = { foo6: "aaa", bar6: "bbb" };
              console.log(baz6);// "aaa"
              //foo6 // error: foo is not defined
              //上面代码中，真正被赋值的是变量baz6，而不是模式foo6
      1.2.5. 对象也可以用于嵌套结构，健用于匹配，赋的其实是值。
      let {p:[x,{y}]}={p:["hello"{"world"}]}
2. 字符串，数字的解构赋值
     2.1. const [a, b, c, d, e] = 'hello';
            console.log(a); // "h"
            console.log(b); // "e"
            console.log(c); // "l"
            console.log(d); // "l"
            console.log(e); // "o"
     2.2. 类数组的对象都有一length属性，对属性也可以解构赋值。
          let {length:len} = "hello";
            console.log(len);
     2.3. 解构赋值，如果等号右边是数值和布尔值，会先转化为对象。
     //解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。
          let {toString: s1} = 123;
          console.log(s1); //
          //s1 === Number.prototype.toString // true
          let {toString: s2} = true;
          console.log(s2); //
          //s2 === Boolean.prototype.toString // true
     2.4. 函数参数的解构赋值
         function a({x=0,y=0}={}){
         return [x,y];
         }
           console.log(a());//[0,0]
           console.log(a({x:1}));[1,0]
           console.log(a(x:1,y:2));[1,2]
         function({x,y}={x:1,y:2}){
         return [x,y];
         }
           console.log(a({}));//underfined underfined
           console.log(a({x:1}));1,underfined
           console.log(a({x:1,y:2}));1,2
3,常见应用
     3.1. 交换应用
        var [x,y]=["a","b"];
            [x,y]=[y,x];
            console.log([x,y]);
     3.2. 从函数中返回多个值
        function a(){
        return {x:1,y:2};
        }
        var {x,y}=a();
        console.log({x,y});
      3.3. 提取JSON对象
        var json = {id:12,a:"ok",data:[12,23]};
        let {id,a,data}=json;
        console.log({id,a,data});
