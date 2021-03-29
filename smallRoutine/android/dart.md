# demo

A new Flutter project.

## 注意事项

- 虚拟设备：实际上是需要Android Studio创建虚拟设备而不是VS Code来创建
- 打开Android Studio,创建模拟器，重复开始步骤

## dart语法

- 注意事项：（特性，语法糖）
    - new 是可选的也就是不写没关系
    - dart字符串是utf-16编码单元，所以用特殊字符Rune表示UTF-32编码字符，\u2665（\u加4个16进制表示，这是个爱心，如果超过4个用{}）
        - 这种特殊符号，单个的用 print(clapping.codeUnits);多个的print(new String.fromCharCodes( new Runes( '\u2665  \u{1f605}'));
    - 函数也是对象，他的类型是function
    - 级联调动：.. 语法为 级联调用，可简化一个对象上执行的多个操作。
        - getOb('#object') //第一步获取对象
        - ..nmae = '${mm}' ;//根据对象调用成员变量
        - ..classes.add(''); //根据对象调用方法
        - 这东西还可以嵌套，不过更难读懂【返回值为void的对象不能创建级联操作】
    - 顶级函数和顶级变量【顶级函数应当相当于顶层函数，也就如同main()一样放置在最上面】
    - 判空，A?.B（A为null，返回null，不然a.b）这样防止空对象调用报空指针错误
    - a.runtimeType返回a对象的属性
    - 实例变量都生成隐式 getter 方法。非 final的实例变量同样会生成隐式 setter 方法
        - 但是可以通过显示的定义 set/get 来覆盖默认值
    - 覆写【操作符】定义写法：
        - 返回类型 operate 操作符(参数1，参数2，...){expression; return;},如果重写==要重写hashcode getter
    - 为类添加功能：Mixin 是复用类代码的一种途径
        - with后面跟一个或多个名称 用，隔开。来使用
        - 通过创建一个没有构造函数的类，来Mixin（如果不想被常规类使用，mixin代替class），on来指定可以使用 Mixin 的父类类型【早期abstract class来代替mixin】：
- 变量
    - 变量就是一个对象。var就行，也可以直接显示声明 string。默认为null（对象一般都是这个）
    - 如果明确说明不需要类型，使用dynamic。比如泛型中，List<dynamic>表示任意类型
    - 关键字
        - 1 上标的单词为上下文关键字，仅在特定位置具有含义。
        - 2 上标的单词为内置标识符，不能用作类
        - 3 上标的单词是异步类
    - 数值只有：int，double 2.1之后是互通的
    - 字符串
        - 对于string 变量，字符串可以通过 ${expression} 的方式内嵌表达式。
        - 三个单引号或者三个双引号实现多行字符串对象的创建：
        - r"\n isn't",r 前缀，可以创建 “原始 raw” 字符串防止转义
- 修饰符
    - 与java不同，没有private，所以标识符_Cc表示相对于库，表示私有
	
    - Final（常量，构造函数之前被初始化）和 Const（Const 变量 是隐式 Final 的类型）
        - final可以先指定，后赋值。const必须先指定（可以 const = const * const指定）
        - const的不可变性是可传递的，final不是，final List ls = [11, 22, 33];ls[1] = 44;//正确const List ls = [11, 22, 33];ls[1] = 44;//错误
        - final会重复创建地址，const不会
        - 实例变量可以是 final 类型但不能是 const 类型（所以const必须在方法里面，如果在类里面必须加 static）
        - const 还可以用于常量，构造函数（声明创建常量值的构造函数），声明可省略
	- typedef 用于方法（一般callBack）和变量，用于变量时会保留类型信息。
	
- 方法（函数）
    - 主函数 main()参数为一个可选的 List<String> 。  程序入口  
    - int转string 1.tostring()，double转string 3.1415.toStringAsFixed(2);(保留两位小数)
    - 可以使用 => 但是这个后面只能跟表达式。
    - 可选参数，函数
        - 可在定义方法的时候 variable = default 的方式来指定默认值【旧版本是：可能会被舍弃】
        - 可选命名myPrint(String cc,{int age,String gend})使用myPrint(cc,age:1,gend:aa)
        - 可选位置myPrint(String cc,[int age,String gend])使用myPrint(cc,1,aa)必须确定位置
        - 如果是字符串内可以 $variable 来指定使用变量
    - 匿名函数
        - var list = ['apples', 'bananas', 'oranges'];这是一个list
        - list.forEach((item) { print('${list.indexOf(item)}: $item');});【里面就是方法，只有一句用表达式】
        - 结果apples bananas oranges （分行）
    - 闭包是一个方法(对象)，定义在其他方法内，可访问外部方法的局部变量
- 数据结构
    - var list = list(2)限定长度【list就相当于array】
        - followedBy(list) 将自身和参数内list合成一个List。list45.followedBy()
        - list18.setRange(0,3, list19);从list19取出0 1 2位置的值，修改list18对应0 1 2
        - replaceRange(1,3,list)范围替换 含头不含尾,1-2(之中的内容包括替换)
    - var list = [1, 2, 3];不能添加非int型的，因为dart推断是int型的
    - var set = <String>{};指定里面的类型。必须加，因为 {} 这个是默认map的只有明确指定 Set set 或者<String>{}。动态声明的时候这样
    - 定义编译时常量 List a = const<String>[], Set b = const{}.因为常量里面要有值，我没放【有add，.length】
    - map的构造函数：var gifts = Map()【也是map对象和上面的那种创建方法应该差不多】; gifts['first'] = 'partridge';
- 运算符
    - 一些稀奇的运算符
		- c = a??b ，a为空，a=b
        - b ??= value;如果为空就赋值，不为空就不赋值
        - 因为这个会自动判断，所以取整assert(5 ~/ 2 == 2); 
        - java中的对象判定 instanceof ，dart是is 不是这个对象就 is！【都表示true】，强制转换 as
        - 自增 ++var，-expr	一元减号，也被命名为负号
- 控制流程
    - dart是不能少break的，所以 fall- through 和java有点区别
    - switch(){case：;;}支持空case， 允许程序以fall-through
    - 非空case实现fall-through
        - case 'CLOSED': executeClosed();continue nowClosed;
        - nowClosed://局部变量。只存在这个作用域
        - case 'NOW_CLOSED':executeNowClosed();break;
    - 断言(assert)，求值结果不满足需要，则打断代码的执行。【生产模式不运行】
- 异常
    - 因为抛出异常是一个表达式， 所以可以在 => 语句中使用
        - 可以抛出任何对象throw 'Out of llamas'
    - 异常捕获（捕获异常可以不用catch，on就够了）
        - java中是try{}catch(){}
        - try{}on Exceptiontype{}catch(e,s)【都一个是异常对象，第二个是栈堆信息】
            - [on可以用来指定类型] on Exception catch (e)什么样的异常什么样的处理
            - catch(){ rethrow;}重新抛出
- 类
    - 构造函数(: 这大概是构造函数前调用吧，也可以跟表达式，最好分段，官网就这样)
        - 要想父类的构造函数在构造函数之前执行 sum(String param):super.father(String param){}
        - 也可以构造函数体之前初始化实例变量 sum(String param):x=3,y='t'{ expression}
        - 命名构造函数 Point.origin() {};point是类名，构造函数
    - 常量构造函数
        - 常量构造函数的定义，其相关成员变量必须为final
        - 如果构造两个相同的常量构造函数会产生唯一的标准实列
    - num x, y;Point(this.x, this.y);// 语法糖已经设置了变量 x 和 y。
    - 工厂构造函数无法访问this。
        - static final Map<String, Logger> _cache = <String, Logger>{};
        - if (_cache.containsKey(name)) { return _cache[name]; }
        - else{final logger = Logger._internal(name);}
    - 扩展类
        - 重写 + 和 - 操作符
            - Vector operator +(Vector v) => Vector(x + v.x, y + v.y);
            - Vector operator -(Vector v) => Vector(x - v.x, y - v.y);
- 接口
    - java中接口就是全是抽象方法的抽象类（接口没有构造方法，抽象有）
        - java8中，可以实现静态方法和普通方法
    - 每个类都隐式的定义了一个接口，所以可以类实现类，
- 泛型 和库】
    - 使用泛型类型的构造函数，类名字后面使用尖括号（<...>）来指定泛型类型
    - <T extends SomeBaseClass>泛型限定
    - 如果导入的库同名，可以 添加 as 名字来识别
    -  延迟加载库{async 和 await 都是异步的}
        - import 'package:greetings/hello.dart' deferred as hello;
        - Future greet() async { await hello.loadLibrary()【加载库】;}
            - 要使用 await，代码必须在 异步函数（使用 async 标记的函数）中：
            - await等待执行，修饰方法等待返回结果再顺序执行，不能用于try catch
            - 要在main()函数使用异步for循环，main函数体必须标记为async
			- 监听Stream，for循环，并把stream对象传入
- 可调用类
    - 实现类的call()方法，类像函数一样被调用。
        - class a{ call(param,param,param) = > 2+3}
        - var c =a()..call(33);//没用本来就是初始化，简单化这样只是赋值
        - a类的实列 c('','','')//初始值，会得到5
- 元数据，注解。注释
    - @override dart自带的就这个
    - dart自定义注解，常量构造函数加@
        - const Todo(this.who, this.what);
        - @Todo("zhangliang", "玩游戏")
        - 文档注释/** * */ 最好是///