# 学习资料

## 大纲
1. iOS基本特性的学习
1. 了解main函数
1. 学习helloworld
1. runtime的学习与理解
1. runloop的学习与理解
1. 学习iOS基本语法以及基本控件的使用（主要项目使用的webview和本地存储）
1. iOS 设计模式的学习（MVC MVVM 代理模式 block 工厂 单列模式等 ）
1. iOS 网络请求的学习（https  socket）
1. iOS 架构的学习
1. iOS 项目调试跟输出控制打印

## 介绍
1. iOS是由苹果公司为iPhone等设备开发的操作体系。它主要是给iPhone、iPod touch和iPad运用。就像其根据的Mac OS X操作体系相同，它也是以Darwin为根底的。iPhone OS的体系架构分为四个层次：中心操作体系层（the Core OS layer），中心效劳层（the Core Services layer），媒体层（the Media layer），可轻触层（the Cocoa Touch layer）。

1. xcode开发：开发iOS运用，需求在Mac OS X运转Xcode开发东西。Xcode是Apple的开发东西套件，撑持项目办理、修改代码、构建可执行程序、代码级调试、代码的版别办理、功用调优等等。这个套件的中心是Xcode运用自身，它供给了根本的源代码开发环境。
1. Interface Builder：运用Interface Builder，能够经过拖拽需求的组件在程序窗口进步行安装。组件中包含规范的体系控件，如开关(switches)、文本框和按钮，还有定制的视图来表明程序供给的视图。在窗口表面上放置组件之后，拖拽它们能够断定方位，运用调查器（inspector）设置它们的特点、树立这些目标和代码之间的联络。当界面是你幻想的那样时，将内容保存在一个nib文件中，这是一个自界说的资源文件格局。

## 开发环境
1. Xcode是Apple自个开发的，只运转在Mac OS X平台下的IDE。运用Xcode来描绘程序的逻辑，运用Interface Builder 来描绘程序的界面。

运转Xcode 3.0或以上的版别需求Mac OS 10.5及以上的体系版别

下载需求注册iOS开发者的账号，登入后即可下载，巨细约为3.5G，包含了XCode、Interface Builder和模拟器等东西。

1. iOS软件开发者证书介绍
啥是软件开发者证书

苹果的开发东西是免费的，可是开发出来的程序需求在真机上运转或许发布到AppStore上（越狱的在外），需求采办苹果的授权。

开发者证书东西即是 Mac 开发者方案成员申请和下载 Mac 运用程序签名证书的东西。采办费用是99美元。它涉及到苹果赞同的条款和条件，并要签署和回来合同。只要注册后才能在iPhone上测验你的程序，而不是在屏幕上的模拟器，一旦你正式变成开发者，你会收到一个证书，有了它你就能够你的设备上运转自个的程序。

苹果为iOS下的开发供给了一系列的撑持，在iOS下开发有着完善的开发言语、东西和撑持体系。一起，苹果对运用软件的维护也给程序员供给了空间，使程序员能够在苹果的平台下享受到软件开发带来的利益。可是许多的约束也给程序员带来不方便，不过这比起iOS体系供给的强壮功用比照就能够承受的。

# 基础语法
## helloworld
1. main方法
  * 每个工程都有一个主函数Main方法这个主函数每次启动都会首先运行
  * int main(int argc, char * argv[])
```
int main(int argc, char * argv[])
{
    NSLog(@"我是main函数的输出语句");
    @autoreleasepool {
        return UIApplicationMain(argc, argv, nil, NSStringFromClass([ZYAppDelegate class]));
    }
}
```
1. 入口类（APPDelegate）
  * 入口类工程函数的入口，一般的初始化操作都放在这里进行。
  * - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

```
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    NSLog(@"我是入口类的方法");

    // window 就是一个主窗口；alloc 申请内存空间，initWithFrame 初始化框架（大小和位置） UIScreen mainScreen  主屏幕 bounds：大小；
    self.window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    // Override point for customization after application launch.
    // 改变窗口的背景颜色
    self.window.backgroundColor = [UIColor redColor];
    // 把设置的window 设置成主键并显示出来；
    [self.window makeKeyAndVisible];

    // 如何创建一个背景：

    // 创建一个对象 并设置图片框架的大小和位置
    UIImageView * iamg=[[UIImageView alloc]initWithFrame:CGRectMake(30, 60, 100, 100)];

    iamg.layer.cornerRadius=50;
    iamg.clipsToBounds=YES;

    // 把图片名字赋值给对象的一个属性
    iamg.image=[UIImage imageNamed:@"Default1.png"];

    //向window上添加这个这个视图；
    [self.window addSubview:iamg];

    return YES;
}
```

## 继承
* oc不支撑多重继承 ，一般子类继承父类，可以重载父类的方法。
* 继承了父类的方法就可以使用父类的方法。

如何创建子类？
创建时选择你需要继承的父类就行创建，那么你就拥有了父类的属性和方法
比如你要创建一个继承于父类为people的person类，你就需要去创建这个类命名为person然后选择父类为people类。
### 导航跳转
* 一般从一个试图跳转到另一个试图有几种方法

1. 找主window，通过找到主window，将主window的rootViewController设置为需要跳转的试图再把设置的window 设置成主键并显示出来；

[self.window makeKeyAndVisible];

1. 通过导航跳转
创建试图控制器的对象然后push过去，前提是需要有导航，返回的使用pop

```
在有导航的情况下直接push过去
ViewController2* VC=[[ViewController2 alloc]init];
    [self.navigationController pushViewController:VC animated:YES];
```

## 控件
### UIButton

```
// 这里创建一个圆角矩形的按钮
    UIButton *button1 = [UIButton buttonWithType:UIButtonTypeRoundedRect];

//    能够定义的button类型有以下6种，
//    typedef enum {
//        UIButtonTypeCustom = 0,          自定义风格
//        UIButtonTypeRoundedRect,         圆角矩形
//        UIButtonTypeDetailDisclosure,    蓝色小箭头按钮，主要做详细说明用
//        UIButtonTypeInfoLight,           亮色感叹号
//        UIButtonTypeInfoDark,            暗色感叹号
//        UIButtonTypeContactAdd,          十字加号按钮
//    } UIButtonType;

    //给定button在view上的位置
    button1.frame = CGRectMake(20, 20, 280, 20);

    //button背景色
    button1.backgroundColor = [UIColor clearColor];

    //设置button填充图片
    //[button1 setImage:[UIImage imageNamed:@"btng.png"] forState:UIControlStateNormal];

    //设置button标题
    [button1 setTitle:@"点击" forState:UIControlStateNormal];

    /* forState: 这个参数的作用是定义按钮的文字或图片在何种状态下才会显现*/
    //以下是几种状态
//    enum {
//        UIControlStateNormal       = 0,         常规状态显现              
//        UIControlStateHighlighted  = 1 << 0,    高亮状态显现    
//        UIControlStateDisabled     = 1 << 1,    禁用的状态才会显现
//        UIControlStateSelected     = 1 << 2,    选中状态              
//        UIControlStateApplication  = 0x00FF0000, 当应用程序标志时            
//        UIControlStateReserved     = 0xFF000000  为内部框架预留，可以不管他             
//    };

    /*
     * 默认情况下，当按钮高亮的情况下，图像的颜色会被画深一点，如果这下面的这个属性设置为no，
     * 那么可以去掉这个功能
    */
    button1.adjustsImageWhenHighlighted = NO;
    /*跟上面的情况一样，默认情况下，当按钮禁用的时候，图像会被画得深一点，设置NO可以取消设置*/
    button1.adjustsImageWhenDisabled = NO;
    /* 下面的这个属性设置为yes的状态下，按钮按下会发光*/
    button1.showsTouchWhenHighlighted = YES;

    /* 给button添加事件，事件有很多种，我会单独开一篇博文介绍它们，下面这个时间的意思是
     按下按钮，并且手指离开屏幕的时候触发这个事件，跟web中的click事件一样。
     触发了这个事件以后，执行butClick:这个方法，addTarget:self 的意思是说，这个方法在本类中
     也可以传入其他类的指针*/
    [button1 addTarget:self action:@selector(butClick:) forControlEvents:UIControlEventTouchUpInside];


    //显示控件
    [self.view addSubview:button1];
```

### UILabel

```
        创建uilabel
        UILabel *label1 = [[UILabel alloc] initWithFrame:CGRectMake(20, 40, 280, 80)];     
        设置背景色
        label1.backgroundColor = [UIColor grayColor];
        设置tag
        label1.tag = 91;
        设置标签文本
        label1.text = @"Hello world!";
        设置标签文本字体和字体大小
        label1.font = [UIFont fontWithName:@"Arial" size:30];
        设置文本对其方式
        label1.textAlignment = UITextAlignmentCenter;
        文本对齐方式有以下三种
        typedef enum {
            UITextAlignmentLeft = 0,左对齐
            UITextAlignmentCenter,居中对齐
            UITextAlignmentRight, 右对齐                  
        } UITextAlignment;
        文本颜色
        label1.textColor = [UIColor blueColor];
        超出label边界文字的截取方式
        label1.lineBreakMode = UILineBreakModeTailTruncation;
        截取方式有以下6种
        typedef enum {
            UILineBreakModeWordWrap = 0,    以空格为边界，保留整个单词          
            UILineBreakModeCharacterWrap,   保留整个字符          
            UILineBreakModeClip,            到边界为止          
            UILineBreakModeHeadTruncation,  省略开始，        
            UILineBreakModeTailTruncation,  省略结尾，      
            UILineBreakModeMiddleTruncation,省略中间，多行时作用于最后一行        
        } UILineBreakMode;
        文本文字自适应大小
        label1.adjustsFontSizeToFitWidth = YES;
        当adjustsFontSizeToFitWidth=YES时候，如果文本font要缩小时
        baselineAdjustment这个值控制文本的基线位置，只有文本行数为1是有效
        label1.baselineAdjustment = UIBaselineAdjustmentAlignCenters;
        有三种方式
        typedef enum {
            UIBaselineAdjustmentAlignBaselines = 0, 默认值文本最上端于label中线对齐
            UIBaselineAdjustmentAlignCenters,//文本中线于label中线对齐
            UIBaselineAdjustmentNone,//文本最低端与label中线对齐
        } UIBaselineAdjustment;
        文本最多行数，为0时没有最大行数限制
        label1.numberOfLines = 2;
        最小字体，行数为1时有效，默认为0.0
        label1.minimumFontSize = 10.0;
        文本高亮
        label1.highlighted = YES;
        文本是否可变
        label1.enabled = YES;
        去掉label背景色
        label1.backgroundColor = [UIColor clearColor];
        文本阴影颜色
        label1.shadowColor = [UIColor grayColor];
        阴影大小
        label1.shadowOffset = CGSizeMake(1.0, 1.0);
        是否能与用户交互
        label1.userInteractionEnabled = YES;
        [self.view addSubview:label1];

```

更多可以访问 http://blog.csdn.net/wolf_hong/article/details/53389406

### UIWebview

```
 //UIWebView：用来加载网页
    UIWebView* webView = [[UIWebView alloc] initWithFrame:self.view.frame];
    //webView上面放了一个scrollView
    //webView.backgroundColor = [UIColor yellowColor];
    //webView.opaque = NO;//透明度
    //webView.scrollView.backgroundColor = [UIColor redColor];
    //webView.scrollView.bounces = NO;//反弹效果
    webView.scalesPageToFit = YES;//自适应大小
    webView.delegate = self;

    //webView的第一个用法
    [webView loadRequest:[NSURLRequest requestWithURL:[NSURL URLWithString:@"http://www.sina.com.cn"]]];

    //webView的第二个用法
    //找本地资源1.获取路径   2.获取资源
//    NSString* filePath = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"html"];
//    //NSUTF8 c语言和oc语言编码
//    NSString* fileResource = [NSString stringWithContentsOfFile:filePath encoding:NSUTF8StringEncoding error:nil];
//    [webView loadHTMLString:fileResource baseURL:nil];
    [self.view addSubview:webView];

    //[webView reload];//重写加载
    //[webView stopLoading];//停止加载
    //[webView goBack];//返回上一个页面
    //[webView goForward];//进去下一个页面

```

## 沙盒机制
### 存储

```
  // 第一种本地存储（直接存储在：library->preferces->plis文件里）
    /*
    // xml --> extended  makeup  language <上海>值</上海>
    // 从本地取出设置皮肤的数据
    NSString* string = [[NSUserDefaults standardUserDefaults] objectForKey:@"ColorType"];
    if (string != nil) {
        [self changeBackgroundColor:[string intValue]];
    }
     */

    // 第二种本地存储（找路径，直接写入）
    NSArray* array = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    //字符串拼接
    NSString* filePath = [[array lastObject] stringByAppendingString:@"/data.plist"];
    //文件路径    //编码格式
    NSString* string = [NSString stringWithContentsOfFile:filePath encoding:NSUTF8StringEncoding error:nil];
    if (string != nil) {
        [self changeBackgroundColor:[string intValue]];
    }
```

### 拼接沙盒路径
1. 存储

```
    // 文件的存储和后缀名没有关系
    // 可以存储的类型：NSString  NSDictionary  NSArray  NSNumbe  NSData  NSDate Boolean

    NSString* filePath = [[self getFilePath] stringByAppendingPathComponent:@"data.plist"];
    //NSString
    //NSString* string  = @"北京";
    //[string writeToFile:filePath atomically:YES encoding:NSUTF8StringEncoding error:nil];

    //NSArray
    //NSArray* arary = @[@"北京"];
    //[arary writeToFile:filePath atomically:YES];

    //NSDictionary
    //NSDictionary* dictionary = @{@"城市": @"北京"};
    //[dictionary writeToFile:filePath atomically:YES];

    //NSNumber* number = [NSNumber numberWithInt:100];
    //NSArray* array = @[number];
    //[array writeToFile:filePath atomically:YES];

    //NSString* string = @"北京";
    // 怎么把一个字符串转化为NSData
    //NSData* data = [string dataUsingEncoding:NSUTF8StringEncoding];
    //[data writeToFile:filePath atomically:YES];


    // ZYPeople类型的可以存储吗？！不能怎么办？答案：不能把自己封装类直接写入到本地，需要通过对象序列化，才能写入！
    ZYPeople* people = [[ZYPeople alloc] init];
    people.name = @"张三";
    people.age = 15;
    NSArray* array = @[people];
    [array writeToFile:filePath atomically:YES];  
```

1. 读取

```
    NSString* filePath = [[self getFilePath] stringByAppendingPathComponent:@"data.plist"];

    //NSString
    //NSString* string = [NSString stringWithContentsOfFile:filePath encoding:NSUTF8StringEncoding error:nil];

    //NSArray
    //NSArray* array = [[NSArray alloc] initWithContentsOfFile:filePath];

    //NSDictionary
    //NSDictionary* dictionary = [NSDictionary dictionaryWithContentsOfFile:filePath];

    //NSData* data = [NSData dataWithContentsOfFile:filePath];
    // 怎么把一个NSData转化成NSString
    //NSString* string = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
    //_label.text = string;
```

1. 得到路径的方法

```
    NSString* filePath = [NSHomeDirectory() stringByAppendingPathComponent:@"Documents"];
    return filePath;
```
