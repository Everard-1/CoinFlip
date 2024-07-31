# CoinFlip
<a name="Qxi2n"></a>
# 创建项目
点击新建项目，选择Qt窗口应用，下一步<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703418701960-448411e5-7a58-46b6-bc92-5863454d1b1b.png#averageHue=%23363a3b&clientId=u29f05a49-994a-4&from=paste&height=599&id=u93762f40&originHeight=1087&originWidth=1764&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=113471&status=done&style=none&taskId=ucb1147af-7e57-41e9-814c-92672c30167&title=&width=971.9007958057247)<br />设置项目名为CoinFlip，注意路径不要有中文，下一步<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703418766899-68ae2ba9-2b37-4351-9a77-dc4ad86590e6.png#averageHue=%23363839&clientId=u29f05a49-994a-4&from=paste&height=577&id=u16b3a43e&originHeight=1047&originWidth=1604&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=83564&status=done&style=none&taskId=u0c2bd9f7-c93e-4dfd-98ca-88a2ea14c7a&title=&width=883.7465286124617)<br />类名为MainScene（主场景），基类为QMainWindow，选择生成界面ui<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703418946128-efee05bc-7ec8-4a30-82ee-89298926e147.png#averageHue=%2337393a&clientId=u29f05a49-994a-4&from=paste&height=577&id=u6ac0c697&originHeight=1047&originWidth=1604&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=83967&status=done&style=none&taskId=ub382d7f9-6846-4ad2-8739-14619135177&title=&width=883.7465286124617)<br />至于其他设置和之前的创建项目一致，完成项目创建后如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703419099124-79823688-3524-4f64-9b7a-607b153cc8c2.png#averageHue=%233a3c3e&clientId=u29f05a49-994a-4&from=paste&height=371&id=u76cadaa5&originHeight=674&originWidth=1412&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=89048&status=done&style=none&taskId=uf03a5343-c6e2-4db1-afa4-0ce4f0e050a&title=&width=777.9614079805461)<br />编译项目，发现创建没有问题<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703419119151-e8fceb07-37f4-48c2-b8ef-07fcde280a5e.png#averageHue=%23efefef&clientId=u29f05a49-994a-4&from=paste&height=356&id=u2d6dccf1&originHeight=647&originWidth=804&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=17931&status=done&style=none&taskId=u79f1fe33-b440-4f47-aeea-e01ba3d1ee7&title=&width=442.97519264614664)

---

<a name="urp2O"></a>
# 添加资源
添加资源和之前类似，先把res文件下复制到项目文件CoinFlip下，然后根据我们之前讲过的导入资源的方法导入资源即可。资源在下：<br />[res.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/27393008/1703421444969-58cdce80-921f-4dc7-90b7-81d294586947.zip)<br />添加后如图所示：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703421470383-4e5a5cf8-13d5-489b-87da-5bac0a9c524b.png#averageHue=%23333739&clientId=u29f05a49-994a-4&from=paste&height=574&id=uf3bd37b7&originHeight=868&originWidth=578&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=77925&status=done&style=none&taskId=u13ac0b43-d264-4ae2-8ce5-c3b1ae78e43&title=&width=382.14874828279517)

---

<a name="zQzGk"></a>
# 项目基本配置
<a name="hO352"></a>
## 配置主场景
下面我们首先配置项目的固定大小、图标和标题
```cpp
    //配置国定大小
    setFixedSize(320,588);

    //设置图标
    setWindowIcon(QIcon(":/res/Coin0001.png"));

    //设置标题
    setWindowTitle("翻金币主场景");
```
<a name="NzdFd"></a>
## 开始——退出菜单实现
我们先在ui中创建好开始菜单的退出选项，并且获取到它的名字`actionquit`。
> 说明：这里的退出刚开始只能输入英文`quit`，然后在右下角的Text中将其设为中文的退出

![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703421855663-598dc86b-9cfd-4c7e-aed8-ebf2b2591372.png#averageHue=%2364b15f&clientId=u29f05a49-994a-4&from=paste&height=548&id=u8f289e9d&originHeight=829&originWidth=1876&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=108030&status=done&style=none&taskId=u8ecf5660-9fff-4bb4-a641-b3bcfc2eec5&title=&width=1240.3305394092106)<br />然后我们用信号槽将其和关闭函数连接起来，实现点击退出结束程序的功能
```cpp
    //退出按钮实现
    connect(ui->actionquit,&QAction::triggered,[=](){
       this->close();
    });
```

---

<a name="GnFtK"></a>
## 绘制背景和背景标题
我们先在主场景的头文件中声明一个绘图函数
```cpp
    //重写paintEvent事件  画背景图
    void paintEvent (QPaintEvent *);
```
然后再在主场景资源文件中重写绘图事件，绘制背景和背景的标题
```cpp
//绘图事件  画背景图
void MainScene::paintEvent(QPaintEvent *)
{
    //画背景
    QPainter painter(this);
    QPixmap pix;
    pix.load(":/res/PlayLevelSceneBg.png");
    painter.drawPixmap(0,0,this->width(),this->height(),pix);

    //画背景上的标题
    pix.load(":/res/Title.png");
    pix = pix.scaled(pix.width()*0.5,pix.height()*0.5);//图标的缩放
    painter.drawPixmap(10,30,pix);

}
```
> 注意：
> - 当背景大小和窗口大小不符时，我们可以在`drawPixmap()`函数中增加两个参数，将背景拉伸为指定宽和高的图片
> - 当图标大小不合适时，我们可以通过调用`scaled()`函数，将其进行缩放然后重新赋值给自己进行绘制


可以看到初步配置后的项目窗口如下所示：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703422581891-64abc8eb-9d78-4f9b-a81c-cc927908363f.png#averageHue=%23c78551&clientId=u29f05a49-994a-4&from=paste&height=420&id=u0556fa80&originHeight=635&originWidth=324&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=406040&status=done&style=none&taskId=u64a3ae2b-4840-43ce-a8a1-188a750d7ce&title=&width=214.2148692796291)

---

<a name="e1FMO"></a>
# 开始按钮创建
<a name="sUgRh"></a>
## 封装自定义按钮MyPushButton
因为Qt中并没有设置按下和弹起两种状态的控件，因此我们只有自定义一个按钮`MyPushButton`，并在Qt中创建好<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703605746845-f94846df-cfa2-4dc8-9a89-24d2d1d43073.png#averageHue=%2338393a&clientId=u89374d8e-563e-4&from=paste&height=692&id=u84d522f1&originHeight=1047&originWidth=1604&originalType=binary&ratio=1.5125000476837158&rotation=0&showTitle=false&size=90426&status=done&style=none&taskId=uc98f489b-6541-4e4d-83e8-bf4c6ba6089&title=&width=1060.495834334954)<br />创建好之后，我们要修改其继承的类，把`QWidget`改为`QPushButton`（修改三处）<br />`mypushbutton.h`中的：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703606946893-f25d55a0-1b47-45e7-ba4f-c8f4155ad430.png#averageHue=%232f3032&clientId=u89374d8e-563e-4&from=paste&height=403&id=u9cf01b4a&originHeight=610&originWidth=1289&originalType=binary&ratio=1.5125000476837158&rotation=0&showTitle=false&size=82936&status=done&style=none&taskId=u81382a2c-3028-4f39-bc04-eaa80f926b6&title=&width=852.2313780908702)<br />`mypushbutton.cpp`中的![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703607009475-a69d2f20-dda8-4186-b827-c659c526122f.png#averageHue=%23303132&clientId=u89374d8e-563e-4&from=paste&height=415&id=u59d4c5ec&originHeight=627&originWidth=1461&originalType=binary&ratio=1.5125000476837158&rotation=0&showTitle=false&size=85617&status=done&style=none&taskId=u73f9fe70-a57e-46e2-bd96-f0391213f57&title=&width=965.9503827701794)
<a name="EQRV1"></a>
## 构造丞数（默认显示图片，按下后显示的图片）
我们注释掉自带的构造函数，声明了一个具有初始默认值的构造函数，因为我们不希望按下后开始按钮切换图片，所以我们默认按下的图片为空。
```cpp
    //explicit MyPushButton(QWidget *parent = nullptr);

    //构造函数 参数1 正常显示的图片路径   参数2 按下后显示的图片路径
    MyPushButton(QString normalImg,QString pressImg="" );

    //成员属性 保存用户传入的默认显示路径 以及按下后显示的图片路径
    QString normalImgPath;
    QString pressImgPath;
```
然后在构造函数中，我们先判断导入图片是否成功，然后再对开始的图标进行了设置

- 设置国定大小——`setFixedSize();`
- 设置不规则图片样式——`setStyleSheet("QPushButton{border:0px;});`
- 设置图标——`setIcon();`
- 设置图标大小——`setIconSize();`
```cpp
MyPushButton::MyPushButton(QString normalImg, QString pressImg)
{
    this->normalImgPath = normalImg;
    this->pressImgPath = pressImg;

    QPixmap pix;
    bool ret = pix.load(normalImg);
    if(!ret){
        qDebug()<<"图片加载失败";
        return;
    }

    //设置图片固定大小
    this->setFixedSize(pix.width(),pix.height());

    //设置不规则图片样式
    this->setStyleSheet("QPushButton{border:0px;}");

    //设置图标
    this->setIcon(pix);

    //设置图标大小
    this->setIconSize(QSize(pix.width(),pix.height()));

}
```
<a name="oNvQb"></a>
## 测试开始按钮
然后我们在主场景函数中实例化开始按钮，并通过`move()`函数，设置开始按钮的位置
```cpp
    //开始按钮
    MyPushButton * startBtn = new MyPushButton(":/res/MenuSceneStartButton.png");
    startBtn->setParent(this);
    startBtn->move(this->width()*0.5 - startBtn->width()*0.5,this->height()*0.7);
```
完成后效果如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703606623615-d7879238-9615-4d06-9764-24d95c88720b.png#averageHue=%23c3824f&clientId=u89374d8e-563e-4&from=paste&height=809&id=ub8bb8b51&originHeight=1223&originWidth=644&originalType=binary&ratio=1.5125000476837158&rotation=0&showTitle=false&size=656735&status=done&style=none&taskId=u5d80f395-9a72-48fe-9e78-ce9e71003ff&title=&width=425.78511054346035)
<a name="HrHd6"></a>
## 开始制作特效
然后我们开始制作按下按钮的弹跳特效，首先我们在`mypushbutton`头文件中，声明两个特效函数
```cpp
    //弹跳特效
    void zoom1();//向下跳
    void zoom2();//向上跳
```
然后我们再分别在cpp文件中实现两个特效函数
<a name="Y9IUH"></a>
## zoom1向下跳
弹跳动画流程：

1. 创建动画对象——`new QPropertyAnimation();`
2. 设置动画时间间隔（ms为单位）——`setDuration();`
3. 设置起始位置——`setStartValue();`
4. 设置结束位置——`setEndValue();`
5. 设置弹跳曲线——`setEasingCurve();`
6. 执行动画——`start();`
```cpp
void MyPushButton::zoom1()
{
    //创建动画对象
    QPropertyAnimation * animation = new QPropertyAnimation(this,"geometry");
    //设置动画时间间隔
    animation->setDuration(200);

    //起始位置
    animation->setStartValue(QRect(this->x(),this->y(),this->width(),this->height()));
    //结束位置
    animation->setEndValue(QRect(this->x(),this->y()+10,this->width(),this->height()));

    //设置弹跳曲线
    animation->setEasingCurve(QEasingCurve::OutBounce);

    //执行动画
    animation->start();
}
```
<a name="sUdy5"></a>
## zoom2向上跳
向下跳和向上跳类似，只是起始和结束位置不同
```cpp
void MyPushButton::zoom2()
{
    //创建动画对象
    QPropertyAnimation * animation = new QPropertyAnimation(this,"geometry");
    //设置动画时间间隔
    animation->setDuration(100);

    //起始位置
    animation->setStartValue(QRect(this->x(),this->y()+10,this->width(),this->height()));
    //结束位置
    animation->setEndValue(QRect(this->x(),this->y(),this->width(),this->height()));

    //设置弹跳曲线
    animation->setEasingCurve(QEasingCurve::OutBounce);

    //执行动画
    animation->start();
}
```
<a name="fYTnf"></a>
## 连接按钮和特效
在主场景中，我们通过信号和槽，实现了点击开始的特效
```cpp
    connect(startBtn,&MyPushButton::clicked,[=](){
        qDebug()<<"点击了开始";
        //做弹起特效
        startBtn->zoom1();
        startBtn->zoom2();
    });
```
效果如下：
[![开始按钮.mp4 (927.93KB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E5%BC%80%E5%A7%8B%E6%8C%89%E9%92%AE.mp4%22%2C%22size%22%3A950205%2C%22taskId%22%3A%22u981f0ce0-b603-47c3-ad7f-06e644041b9%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2023%2F27393008%2Fmp4%2F1703607801805-ba341700-48c5-4481-9292-ea936a963b75.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22ZcAxN%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#ZcAxN)
---

<a name="hry3X"></a>
# 选择关卡场景配置
<a name="dHXRx"></a>
## 创建选择关卡类
首先我们先创建一个`ChooseLevelScene`类<br />![image.png](https://cdn.nlark.com/yuque/0/2023/png/27393008/1703671275573-2c351726-7c59-44a8-bd26-cba4544ba884.png#averageHue=%2338393b&clientId=u93d4b6a3-7f0d-4&from=paste&height=692&id=uee22b151&originHeight=1047&originWidth=1604&originalType=binary&ratio=1.5125000476837158&rotation=0&showTitle=false&size=91126&status=done&style=none&taskId=u6525aeb8-1397-4b9b-8f3d-fc5e6101eeb&title=&width=1060.495834334954)<br />然后在主场景中实例化选择关卡场景
```cpp
    //实例化选择关卡场景
    chooseScene = new ChooseLevelScene;
```
<a name="WaayE"></a>
## 延时进入选择关卡场景
因为点击开始后，就需要切换场景，所以我们的代码还是写在之前的信号槽函数中。

- 延时——`QTimer::singleShot();`
- 关闭当前窗口——`this->hide();`
- 显示选择关卡场景——`chooseScene->show();`
```cpp
        //延时进入选择关卡场景中
        QTimer::singleShot(500,this,[=](){
            //自身隐藏
            this->hide();
            //显示选择关卡场景
            chooseScene->show();
        });
```
<a name="NOfiD"></a>
## 配置选择关卡场景
此时我们切换后的场景是一个空的大小不符合要求的窗口，下面我们在`ChooseLevelScene.cpp`中配置这个窗口。<br />我们按照之前在主场景中设置的方式同样的在选择关卡中设置窗口大小、图标、标题、和菜单栏等。
```cpp
ChooseLevelScene::ChooseLevelScene(QWidget *parent) : QMainWindow(parent)
{
    //配置选择关卡场景
    this->setFixedSize(320,588);

    //设置图标
    this->setWindowIcon(QPixmap(":/res/Coin0001.png"));

    //设置标题
    this->setWindowTitle("选择关卡场景");

    //创建菜单栏
    QMenuBar *bar = menuBar();
    setMenuBar(bar);

    //创建开始菜单
    QMenu * startMenu = bar->addMenu("开始");

    //创建退出 菜单项
    QAction * quitAction = startMenu->addAction("退出");

    //点击退出 实现退出游戏
    connect(quitAction,&QAction::triggered,[=](){
        this->close();
    });
}
```
<a name="HyX63"></a>
## 设置背景、标题图片
但此时我们的窗口下面仍然是空白的，下面我们就需要加载背景和标题<br />我们现在其头文件中重新声明一个绘制事件
```cpp
    //重写绘图事件
    void paintEvent(QPaintEvent *);
```
然后我们在其资源文件中实现绘图事件
```cpp
void ChooseLevelScene::paintEvent(QPaintEvent *)
{
    //画背景
    QPainter painter(this);
    QPixmap pix;
    pix.load(":/res/OtherSceneBg.png");
    painter.drawPixmap(0,0,this->width(),this->height(),pix);

    //画背景上的标题
    pix.load(":/res/Title.png");
    painter.drawPixmap(this->width()*0.5-pix.width()*0.5,30,pix);
}
```
<a name="OK7ad"></a>
## 创建返回按钮
这样我们就得到了有背景和标题的窗口，下面我们继续制作返回按钮<br />我们使用之前的`MyPushButton`类创建一个返回按钮，设置好它在窗口中的位置后，我们先简单的让他dubug
```cpp
    //返回按钮
    MyPushButton * backBtn = new MyPushButton(":/res/BackButton.png",":/res/BackButtonSelected.png");
    backBtn->setParent(this);
    backBtn->move(this->width()-backBtn->width(),this->height()-backBtn->height());

    //点击返回
    connect(backBtn,&MyPushButton::clicked,[=](){
        qDebug()<<"点击了返回";
```
<a name="PQabb"></a>
## 实现返回按钮图片切换
我们先在`mypushbutton.h`中重写按钮的按下和释放事件
```cpp
    //重写按钮 按下 和 释放事件
    void mousePressEvent (QMouseEvent *e);

    void mouseReleaseEvent (QMouseEvent *e);
```
然后在实现中判断是否有切换的图片。然后分别切换为按下图片和初始图片
```cpp
void MyPushButton::mousePressEvent(QMouseEvent *e)
{
    //如果传入图片不为空 说明需要有按下状态，切换为初始图片
    if(this->pressImgPath!=""){
        QPixmap pix;
        bool ret = pix.load(this->pressImgPath);
        if(!ret){
            qDebug()<<"图片加载失败";
            return;
        }

        //设置图片固定大小
        this->setFixedSize(pix.width(),pix.height());

        //设置不规则图片样式
        this->setStyleSheet("QPushButton{border:0px;}");

        //设置图标
        this->setIcon(pix);

        //设置图标大小
        this->setIconSize(QSize(pix.width(),pix.height()));
    }

    //让父类执行其他内容
    return QPushButton::mousePressEvent(e);
}
```
```cpp
void MyPushButton::mouseReleaseEvent(QMouseEvent *e)
{
    //如果传入图片不为空 说明需要有按下状态，切换初始图片
    if(this->pressImgPath!=""){
        QPixmap pix;
        bool ret = pix.load(this->normalImgPath);
        if(!ret){
            qDebug()<<"图片加载失败";
            return;
        }

        //设置图片固定大小
        this->setFixedSize(pix.width(),pix.height());

        //设置不规则图片样式
        this->setStyleSheet("QPushButton{border:0px;}");

        //设置图标
        this->setIcon(pix);

        //设置图标大小
        this->setIconSize(QSize(pix.width(),pix.height()));
    }

    //让父类执行其他内容
    return QPushButton::mouseReleaseEvent(e);
}
```
效果如下：
[![返回按钮.mp4 (1.58MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E8%BF%94%E5%9B%9E%E6%8C%89%E9%92%AE.mp4%22%2C%22size%22%3A1661823%2C%22taskId%22%3A%22u5a421738-fd6b-42e3-8ace-a4b42333e75%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2023%2F27393008%2Fmp4%2F1703675839598-c8a8e5e9-552f-496f-bb84-fafb61e0252b.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22ToIxb%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#ToIxb)<a name="XYuJ3"></a>
# 开始场景和选择关卡场景切换
我们要实现点击选择关卡的返回，返回到主场景界面
<a name="S0I3P"></a>
## 自定义信号
我们需要选择关卡场景释放一个信号，然后由主场景来监听，是否需要返回到主场景。<br />首先我们先在`chooselevelscene.h`中自定义一个信号
```cpp
signals:
    //写一个自定义信号，告诉主场景  点击了返回
    void chooseSceneBack();
```
然后我们在返回按键的信号和槽函数中，发送这个信号——`emit();`，同样的我们可以选择延时发送信号。
```cpp
    //点击返回
    connect(backBtn,&MyPushButton::clicked,[=](){
        //告诉主场景 我返回了 主场景监听ChooseLevelScene的返回按钮
        //延时返回
        QTimer::singleShot(0,this,[=](){
            emit this->chooseSceneBack();
        });
```
<a name="KOkwc"></a>
## 连接主场景和信号
因为我们只需要连接信号和槽一次，所以我们不把它写在开始的信号和槽函数中，而是写在外面的构造函数中
```cpp
    //监听选择关卡的返回按钮的信号
    connect(chooseScene,&ChooseLevelScene::chooseSceneBack,this,[=](){
        chooseScene->hide();//把选择关卡的场景  关闭掉
        this->show();//重新显示主场景
    });
```
通过检测这个信号，我们就可以返回到主场景了，效果如下：
[![返回主场景.mp4 (2.54MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E8%BF%94%E5%9B%9E%E4%B8%BB%E5%9C%BA%E6%99%AF.mp4%22%2C%22size%22%3A2665359%2C%22taskId%22%3A%22u0727c05d-d3a5-44f8-8b0c-2c14ab1ec50%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2023%2F27393008%2Fmp4%2F1703683110917-c75c3a76-76a7-4d62-86a9-0749be35a7a4.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22dXYhE%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#dXYhE)
---

<a name="xsGrx"></a>
# 创建选择关卡中的按钮
<a name="pfi2U"></a>
## 布置按钮到场景
我们通过一个for循环加上 % 和 / 实现了一个二维矩阵，让按钮分布到不同的位置了。
```cpp
    //创建选择关卡的按钮
    for(int i=0;i<20;i++){
        MyPushButton * menuBtn = new MyPushButton(":/res/LevelIcon.png");
        menuBtn->setParent(this);
        menuBtn->move(i%4 * 70 + 25, i/4 *70 + 130);
    }
```
<a name="OAu6q"></a>
## 显示关卡数
因为按钮是不规则的图形，如果我们直接在按钮上设置文本，那么会显示错误i<br />因此，我们直接创建Label，让其覆盖在按钮的上方，但是因为和按钮大小相同，所以默认在最左边，因此我们需要设置对齐方式，让其处于中心位置
```cpp
        QLabel * label = new QLabel;
        label->setParent(this);
        label->setFixedSize(menuBtn->width(),menuBtn->height());
        label->setText(QString::number(i+1));
        label->move(i%4 * 70 + 25, i/4 *70 + 130);

        //设置 label上的文字对齐方式
        label->setAlignment(Qt::AlignCenter | Qt::AlignVCenter);
```
<a name="ZjwRv"></a>
## 监听每个按钮的点击事件
我们通过信号和槽函数，获取到选择的是哪一个关卡，但是因为label覆盖在按钮的上方，鼠标点击被label拦截了，因此我们需要设置，让鼠标具有穿透力，让其作用于按钮上。
```cpp
        //监听每个按钮的点击事件
        connect(menuBtn,&MyPushButton::clicked,[=](){
            QString str = QString("您选择的是第 %1 关").arg(i+1);
            qDebug()<<str;
        });
        //设置让鼠标进行穿透
        label->setAttribute(Qt::WA_TransparentForMouseEvents);
```
效果如下：
[![选择关卡按钮.mp4 (4.93MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E9%80%89%E6%8B%A9%E5%85%B3%E5%8D%A1%E6%8C%89%E9%92%AE.mp4%22%2C%22size%22%3A5169520%2C%22taskId%22%3A%22u1b9d9650-d71e-487e-8882-d748f79d017%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2023%2F27393008%2Fmp4%2F1703686091107-5ef2a155-8b13-4eed-b71f-dcd9c80703d6.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22WEwUH%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#WEwUH)
---

<a name="NfMkO"></a>
# 翻金币场景创建
<a name="OI4gg"></a>
## 进入翻金币游戏场景
先创建一个翻金币场景类`PlayScene`，我们在选择场景中创建一个游戏场景并显示
```cpp
            //进入到游戏场景
            this->hide();//将选关场景关闭
           play = new PlayScene(i+1);//创建游戏场景
           play->show();//显示游戏场景
```
但是我们的构造函数参数并非int型，所以我们还要自己重写一个构造函数
```cpp
public:
    //explicit PlayScene(QWidget *parent = nullptr);

    PlayScene(int levelNum);

    int levelIndex;//内部成员属性  记录所选的关卡
```
```cpp
PlayScene::PlayScene(int levelNum)
{
    QString str = QString("进入了第%1关").arg(levelNum);
    qDebug()<<str;
    this->levelIndex=levelNum;
}
```
<a name="hggPe"></a>
## 配置翻金币游戏场景
我们先配置图标和菜单栏等部分
```cpp
    //初始化游戏场景
    //设置固定大小
    this->setFixedSize(320,588);
    //设置图标
    this->setWindowIcon(QPixmap(":/res/Coin0001.png"));
    //设置标题
    this->setWindowTitle("翻金币场景");

    //创建菜单栏
    QMenuBar *bar = menuBar();
    setMenuBar(bar);

    //创建开始菜单
    QMenu * startMenu = bar->addMenu("开始");

    //创建退出 菜单项
    QAction * quitAction = startMenu->addAction("退出");
    //点击退出 实现退出游戏
    connect(quitAction,&QAction::triggered,[=](){
        this->close();
    });

```
然后再重写一个绘图事件，用来绘制背景
```cpp
    //重写painterEvent事件
    void paintEvent(QPaintEvent *);
```
```cpp
void PlayScene::paintEvent(QPaintEvent *)
{
    //创建背景
    QPainter painter(this);

    QPixmap pix;
    pix.load(":/res/PlayLevelSceneBg.png");
    painter.drawPixmap(0,0,this->width(),this->height(),pix);

    //加载标题
    pix.load(":/res/Title.png");
    pix = pix.scaled(pix.width()*0.5,pix.height()*0.5);
    painter.drawPixmap(10,30,pix.width(),pix.height(),pix);
}
```
<a name="Wnz7w"></a>
## 实现返回按钮
对于返回按钮，我们定义一个自定义信号
```cpp
signals:
    void chooseSceneBack();
```
然后我们设置一个按钮，让其发出信号
```cpp
    //返回按钮
    MyPushButton  * backBtn = new MyPushButton(":/res/BackButton.png" , ":/res/BackButtonSelected.png");
    backBtn->setParent(this);
    backBtn->move(this->width()-backBtn->width(),this->height()-backBtn->height());

    //点击返回
    connect(backBtn,&MyPushButton::clicked,[=](){
        //告诉主场景 我返回了 主场景监听ChooseLevelScene的返回按钮
        //延时返回
        qDebug()<<"翻金币场景中点击了返回按钮";
        QTimer::singleShot(0,this,[=](){
            emit this->chooseSceneBack();
        });
    });
```
然后我们实现接受信号，返回上一场景
```cpp
           connect(play,&PlayScene::chooseSceneBack,[=](){
               this->show();
               delete play;
               play = NULL;
           });
```

---

<a name="EDVIe"></a>
# 实现显示关卡标签
我们创建一个标签，显示当前关卡的数目，并通过QFont改变标签的字体和字号
```cpp
    //显示当前关卡数
    QLabel * label = new QLabel;
    label->setParent(this);
    QFont font;
    font.setFamily("华文新魏");
    font.setPointSize(20);
    QString str2 = QString("Level: %1").arg(this->levelIndex);
    //将字体设置到标签控件中
    label->setFont(font);
    label->setText(str2);
    label->setGeometry(30,this->height()-50,120,50);
```
效果如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/27393008/1705123419143-f6a9db01-bb9d-4064-a93e-0ad4af097f86.png#averageHue=%23c7824e&clientId=u14205171-ac47-4&from=paste&height=674&id=uf3fb75df&originHeight=1223&originWidth=644&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=627058&status=done&style=none&taskId=u4b17f0ae-2b8a-41da-ac09-df7a7994f8a&title=&width=354.8209254528836)

---

<a name="S8H7b"></a>
# 创建金币类
<a name="Oq9sv"></a>
## 绘制金币背景图案
我们先把金币的背景图案在`PlayScene`中绘制出来
```cpp
    //显示金币背景图案
    for(int i=0;i<4;i++){
        for(int j=0;j<4;j++){
            //绘制背景图片
            QPixmap pix = QPixmap(":/res/BoardNode(1).png");
            QLabel *label = new QLabel;
            label->setGeometry(0,0,pix.width(),pix.height());
            label->setPixmap(pix);
            label->setParent(this);
            label->move(57+i*50,200+j*50);
        }
    }
```
<a name="RvSXE"></a>
## 创建自定义金币按钮类
我们先创建继承于QWidget的`MyCoin`类，将其修改为为继承于QPushButton类<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/27393008/1705127104543-a0dfeb81-cfc9-413d-be90-fa28729c2e6a.png#averageHue=%23313234&clientId=u14205171-ac47-4&from=paste&height=289&id=u43f8298f&originHeight=525&originWidth=893&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=49437&status=done&style=none&taskId=u02f83f9e-e466-4cc4-90d1-3c20d9ceecf&title=&width=492.0110037723992)![image.png](https://cdn.nlark.com/yuque/0/2024/png/27393008/1705127132274-ced5d300-507a-419d-a01b-8942660c493b.png#averageHue=%232f3031&clientId=u14205171-ac47-4&from=paste&height=172&id=u38def0d5&originHeight=312&originWidth=1042&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=22340&status=done&style=none&taskId=u447b4e16-900e-43b8-b7b3-5b01293f1a5&title=&width=574.1046650961254)
<a name="SivCN"></a>
## 在构造函数中加载金币图片
我们在金币按钮类中自定义一个构造函数
```cpp
    //参数代表 传入的金币路径 还是银币路径
    MyCoin(QString btnImg);
```
然后在构造函数中加载金币的图片并设置金币图片的大小
```cpp
MyCoin::MyCoin(QString btnImg)
{
    QPixmap pix;
    bool ret = pix.load(btnImg);
    if(!ret){
        QString str = QString("图片%1加载失败").arg(btnImg);
        qDebug()<<str;
        return;
    }

    this->setFixedSize(pix.width(),pix.height());
    this->setStyleSheet("QPushButton{border:0px;}");
    this->setIcon(pix);
    this->setIconSize(QSize(pix.width(),pix.height()));
}

```
<a name="PEJ07"></a>
## 在游戏场景中创建所有金币
我们在创建金币背景中的循环中也创建金币
```cpp
            //创建金币
            MyCoin * coin = new MyCoin(":/res/Coin0001.png");
            coin->setParent(this);
            coin->move(59+i*50,204+j*50);
```
效果如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/27393008/1705127651790-20bf2f6a-d18d-4b05-a748-ab9fb695eed4.png#averageHue=%23bc7b40&clientId=u14205171-ac47-4&from=paste&height=674&id=u09361afd&originHeight=1223&originWidth=644&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=609445&status=done&style=none&taskId=ubeef49f9-00d1-41c9-b23a-75a3cdc45bc&title=&width=354.8209254528836)

---

<a name="NTAix"></a>
# 每个关卡的默认显示
<a name="s0OND"></a>
## 添加文件
先将两个文件放入项目文件夹，然后选择添加现有文件，添加到项目中<br />[dataconfig.cpp](https://www.yuque.com/attachments/yuque/0/2024/txt/27393008/1705129130073-fab6ed94-9a14-44e5-9df0-2ab6001ce78a.txt)<br />[dataconfig.h](https://www.yuque.com/attachments/yuque/0/2024/txt/27393008/1705129130081-dab2a555-a644-4390-8851-a222eef7abf1.txt)
<a name="p8C2a"></a>
## 初始化每个关卡的二维数组
我们在游戏场景中初始化每个关卡的初始二维数组
```cpp
    //初始化每个关卡的二维数组
    dataConfig config;
    for(int i=0;i<4;i++){
        for(int j=0;j<4;j++){
            this->gameArray[i][j] = config.mData[this->levelIndex][i][j];
        }
    }
```
<a name="Bw7cR"></a>
## 显示默认金币效果
然后我们根据二维数组的值确定金币的颜色，进行显示
```cpp
            //创建金币
            QString str;
            if(this->gameArray[i][j]==1){
                str = ":/res/Coin0001.png";
            }
            else{
                str = ":/res/Coin0008.png";
            }
            MyCoin * coin = new MyCoin(str);
            coin->setParent(this);
            coin->move(59+i*50,204+j*50);
```
效果如下：<br />![image.png](https://cdn.nlark.com/yuque/0/2024/png/27393008/1705131107672-ee92de25-4062-45e7-90b1-6a250732cbcf.png#averageHue=%23bc7b45&clientId=u14205171-ac47-4&from=paste&height=674&id=u9883e5a5&originHeight=1223&originWidth=644&originalType=binary&ratio=1.815000057220459&rotation=0&showTitle=false&size=629964&status=done&style=none&taskId=u02dfa069-5825-4949-bce2-3f4a0c4db44&title=&width=354.8209254528836)

---

<a name="N8x6n"></a>
# 金币翻转效果
<a name="jXgQD"></a>
## 给金币添加属性
我们先给金币添加x坐标、y坐标和正反面标志flag三个属性
```cpp
    //金币的属性
    int posX;//x坐标位置
    int posY;//y坐标位置
    bool flag;//正反标示
```
<a name="IiQcc"></a>
## 声明翻转函数
我们声明一个用于翻转金币状态的函数，并创建两个定时器，设置最小值和最大值用于制作动画
```cpp
    //改变标志的方法
    void changeFlag();
    QTimer * timer1;//正面翻反面的定时器
    QTimer * timer2;//反面翻正面的定时器
    int min=1;
    int max=8;
```
<a name="L0c5R"></a>
## 实现翻转函数
我们先初始化两个定时器对象
```cpp
    //初始化定时器对象
    timer1 = new QTimer(this);
    timer2 = new QTimer(this);
```
然后我们分别检验金币的状态，并选择触发timer1或timer2
```cpp
//改变正反面标志的方法
void MyCoin::changeFlag()
{
    //如果是正面  翻成反面
    if(this->flag){
        //开始正面翻反面的定时器
        timer1->start(30);
        this->flag=false;
    }
    //反面翻正面
    else{
        timer2->start(30);
        this->flag=true;
    }
}
```
然后我们用两个槽函数分别接收timer1和timer2的信号，让图片逐个被加载
```cpp
    //监听正面翻反面的信号，并且翻转金币
    connect(timer1,&QTimer::timeout,[=](){
        QPixmap pix;
        QString str = QString(":/res/Coin000%1.png").arg(min++);
        pix.load(str);

        this->setFixedSize(pix.width(),pix.height());
        this->setStyleSheet("QPushButton{border:0px;}");
        this->setIcon(pix);
        this->setIconSize(QSize(pix.width(),pix.height()));

        //判断 如果翻完了，将min设置为1
        if(this->min>this->max){
            this->min = 1;
            timer1->stop();
        }
    });

    //监听反面翻正面的信号，并且翻转金币
    connect(timer2,&QTimer::timeout,[=](){
        QPixmap pix;
        QString str = QString(":/res/Coin000%8.png").arg(max--);
        pix.load(str);

        this->setFixedSize(pix.width(),pix.height());
        this->setStyleSheet("QPushButton{border:0px;}");
        this->setIcon(pix);
        this->setIconSize(QSize(pix.width(),pix.height()));

        //判断 如果翻完了，将min设置为1
        if(this->max<this->min){
            this->max = 8;
            timer2->stop();
        }
    });
```
<a name="G6yPi"></a>
## 实现点击金币翻转
实现了翻转效果后，我们要把点击和翻转用信号和槽函数连接起来，实现点击金币翻转
```cpp
            //点击金币进行翻转
            connect(coin,&MyCoin::clicked,[=](){
                coin->changeFlag();
            });
```
效果如下：
[![金币翻转.mp4 (3.29MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E9%87%91%E5%B8%81%E7%BF%BB%E8%BD%AC.mp4%22%2C%22size%22%3A3450735%2C%22taskId%22%3A%22u35aa2e94-4ef2-4fca-bf55-456b7d9ba2d%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2024%2F27393008%2Fmp4%2F1705133906231-3c8b8852-1980-48a0-a0ca-c1e9bb368b1e.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22rXOCC%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#rXOCC)
---

<a name="KIcjB"></a>
# 翻转周围金币
因为无法获取到每个金币的坐标，所以我们单独把它们保存到一个二维数组中
```cpp
    MyCoin * coinBtn[4][4];
```
同时我们再翻转金币的信号和槽函数中，同时延时翻转该金币的周围金币
```cpp
                //翻转周围硬币
                QTimer::singleShot(300,this,[=](){
                    if(coin->posX+1<=3){//周围的右侧金币翻转的条件
                        coinBtn[coin->posX+1][coin->posY]->changeFlag();
                        this->gameArray[coin->posX+1][coin->posY] = this->gameArray[coin->posX+1][coin->posY] == 0 ? 1: 0;
                    }
                    //周围左侧硬币翻转条件
                    if(coin->posX-1>=0){
                        coinBtn[coin->posX-1][coin->posY]->changeFlag();
                        this->gameArray[coin->posX-1][coin->posY] = this->gameArray[coin->posX-1][coin->posY] == 0 ? 1: 0;
                    }
                    //周围上侧的硬币翻转条件
                    if(coin->posY+1<=3){
                        coinBtn[coin->posX][coin->posY+1]->changeFlag();
                        this->gameArray[coin->posX][coin->posY+1] = this->gameArray[coin->posX][coin->posY+1] == 0 ? 1: 0;
                    }
                    //周围下侧的硬币翻转条件
                    if(coin->posY-1>=0){
                        coinBtn[coin->posX][coin->posY-1]->changeFlag();
                        this->gameArray[coin->posX][coin->posY-1] = this->gameArray[coin->posX][coin->posY-1] == 0 ? 1: 0;
                    }
                });
```
效果如下：
[![翻转周围金币.mp4 (1.48MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E7%BF%BB%E8%BD%AC%E5%91%A8%E5%9B%B4%E9%87%91%E5%B8%81.mp4%22%2C%22size%22%3A1554408%2C%22taskId%22%3A%22u8b6b0f8c-12eb-4b9f-a067-5449207b477%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2024%2F27393008%2Fmp4%2F1705141880861-59f34e87-a465-4c30-be5b-0803855a0569.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22U74I4%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#U74I4)
---

<a name="xNA6v"></a>
# 判断游戏胜利
<a name="gWXoE"></a>
## 添加isWin的标志
首先我们在`mycoin.h`和`playscene.h`中声明并初始化胜利标志
```cpp
    //是否胜利的标志
    bool isWin = false;
```
```cpp
    //是否胜利的标志
    bool isWin = false;
```
<a name="U9AJm"></a>
## 判断是否胜利
我们需要在每一次翻转金币后判断是否胜利，因此我们将其写在延迟翻转中的匿名函数
```cpp
                    //判断是否胜利
                    this->isWin = true;
                    for(int i=0;i<4;i++){
                        for(int j=0;j<4;j++){
                            if(coinBtn[i][j]->flag == false)//只有一个是反面，那就算失败
                            {
                                this->isWin = false;
                                break;
                            }
                        }
                    }
                    if(this->isWin == true){
                        //胜利了
                        qDebug()<<"游戏胜利";
                    }
```
<a name="jXNqr"></a>
## 胜利后屏蔽算法点击
在胜利后，我们把所有金币标志设置为true
```cpp
                    if(this->isWin == true){
                        //胜利了
                        qDebug()<<"游戏胜利";
                        //将所有按钮的胜利标志改为true,如果再次点击按钮，直接return，不做响应
                        for(int i=0;i<4;i++){
                            for(int j=0;j<4;j++){
                                coinBtn[i][j]->isWin=true;
                            }
                        }
                    }
```
当胜利标志为true后，点击金币直接return不做响应
```cpp
void MyCoin::mousePressEvent(QMouseEvent *e)
{
    if(this->isAnimation==true || this->isWin){
        return;
    }
    else{
        QPushButton::mousePressEvent(e);
    }
}

```
效果如下：
[![胜利效果.mp4 (4.44MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E8%83%9C%E5%88%A9%E6%95%88%E6%9E%9C.mp4%22%2C%22size%22%3A4656919%2C%22taskId%22%3A%22ue8c883c6-deb3-4430-90a3-4cfded6a689%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2024%2F27393008%2Fmp4%2F1705151639930-d2eaf633-e615-4e61-93ce-8d8d8d338d80.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22CtstF%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#CtstF)
---

<a name="OOA47"></a>
# 胜利图片效果
<a name="pZ27H"></a>
## 将胜利图片放到游戏场景上方外
因为胜利图片在胜利之前是看不见的，因此我们把它写在外面
```cpp
    //胜利图片显示
    QLabel * winLabel = new QLabel;
    QPixmap tmpPix;
    tmpPix.load(":/res/LevelCompletedDialogBg.png");
    winLabel->setGeometry(0,0,tmpPix.width(),tmpPix.height());
    winLabel->setPixmap(tmpPix);
    winLabel->setParent(this);
    winLabel->move((this->width()-tmpPix.width())*0.5,-tmpPix.height());
```
<a name="v1pP0"></a>
## 将胜利图片移到中央
因为我们在游戏胜利后才把图片移到中央，因此我们把代码写在判断游戏胜利的条件语句中
```cpp
                        //将胜利的图片移动下来
                        QPropertyAnimation * animation = new QPropertyAnimation(winLabel,"geometry");
                        //设置时间间隔
                        animation->setDuration(1000);
                        //设置开始位置
                        animation->setStartValue(QRect(winLabel->x(),winLabel->y(),winLabel->width(),winLabel->height()));
                        //设置结束位置
                        animation->setEndValue(QRect(winLabel->x(),winLabel->y()+144,winLabel->width(),winLabel->height()));
                        //设置缓和曲线
                        animation->setEasingCurve(QEasingCurve::OutBounce);
                        //执行动画
                        animation->start();
```
效果如下：
[![胜利图片.mp4 (2.92MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E8%83%9C%E5%88%A9%E5%9B%BE%E7%89%87.mp4%22%2C%22size%22%3A3063009%2C%22taskId%22%3A%22u703141c6-2059-4aeb-aa24-453337b5580%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2024%2F27393008%2Fmp4%2F1705211903001-5d098273-46d8-4720-be13-eec26f5c795a.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22Pt4F2%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#Pt4F2)
---

<a name="zgRWP"></a>
# 添加音效
<a name="vfZZu"></a>
## 添加多媒体模块
添加音效需要使用`#include <QSound>`头文件，但是其属于多媒体模块，我们需要在.pro文件中加入这个模块
```cpp
QT       += core gui multimedia
```
<a name="VRNVj"></a>
## 添加主场景音效
我们先在主场景中准备好开始按钮的音效
```cpp
    //准备开始按钮的音效
    QSound * startSound = new QSound(":/res/TapButtonSound.wav",this);
```
然后我们在开始按钮的信号和槽函数中，加入音效，这样点击了按钮后就会播放音效
```cpp
        //播放开始音效资源
//        startSound->setLoops(-1);//设置循环，如果是-1，代表无限循环
        startSound->play();
```
<a name="WfE0e"></a>
## 添加选择场景音效
类比于开始按钮，我们添加选择场景中的音效
```cpp
    //选择关卡按钮音效
    QSound * chooseSound = new QSound(":/res/TapButtonSound.wav",this);
    //返回按钮音效
    QSound * backSound = new QSound(":/res/BackButtonSound.wav",this);
```
分别在返回按钮和选择按钮信号和槽函数中使用音效
```cpp
        //返回按钮音效
        backSound->play();
```
```cpp
            //播放选择关卡音效
            chooseSound->play();
```
<a name="R3Jcv"></a>
## 添加游戏场景中的音效
```cpp
    //添加音效资源
    //返回按钮音效
    QSound * backSound = new QSound("/res/BackButtonSound.wav",this);
    //翻金币音效
    QSound * flipSound = new QSound(":/res/ConFlipSound.wav",this);
    //胜利按钮音效
    QSound * winSound = new QSound(":/res/LevelWinSound.wav",this);
```
```cpp
        //返回按钮音效
        backSound->play();
```
```cpp
                //点击金币音效
                flipSound->play();

```
```cpp
                        //游戏胜利音效
                        winSound->play();
```
效果如下：
[![游戏音效.mp4 (7.1MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E6%B8%B8%E6%88%8F%E9%9F%B3%E6%95%88.mp4%22%2C%22size%22%3A7449644%2C%22taskId%22%3A%22u6077b16e-bafd-4a97-ad87-732b377b0a6%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2024%2F27393008%2Fmp4%2F1705223177077-38963b5a-0979-4f3a-a2b1-eb46070f6e77.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22G2WbX%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#G2WbX)
---

<a name="oTdHN"></a>
# 项目优化
<a name="yUCne"></a>
## 统一主界面和选择界面位置
我们把进入选择场景的界面位置设置为当前界面位置
```cpp
            //设置chooseScene场景的位置
            chooseScene->setGeometry(this->geometry());
```
当点击返回时，我们又把主界面位置设为选择界面位置
```cpp
        this->setGeometry(chooseScene->geometry());
```
<a name="Uywvy"></a>
## 统一选择界面和游戏界面位置
我们把游戏场景位置设为当前位置，它应该在创建场景之后、显示场景之前设置
```cpp
           //设置游戏场景的初始位置
           play->setGeometry(this->geometry());
```
当点击返回时，我们把选择场景位置设置为游戏场景位置
```cpp
               this->setGeometry(play->geometry());
```
效果如下：
[![场景位置优化.mp4 (21.41MB)](https://gw.alipayobjects.com/mdn/prod_resou/afts/img/A*NNs6TKOR3isAAAAAAAAAAABkARQnAQ)](https://www.yuque.com/docs/150058640?_lake_card=%7B%22status%22%3A%22done%22%2C%22name%22%3A%22%E5%9C%BA%E6%99%AF%E4%BD%8D%E7%BD%AE%E4%BC%98%E5%8C%96.mp4%22%2C%22size%22%3A22447200%2C%22taskId%22%3A%22u09b1773f-79fc-4e5b-b12d-7d6ddb07d26%22%2C%22taskType%22%3A%22upload%22%2C%22url%22%3Anull%2C%22cover%22%3Anull%2C%22videoId%22%3A%22inputs%2Fprod%2Fyuque%2F2024%2F27393008%2Fmp4%2F1705224656704-de018af3-28c0-4385-a48f-506ddd17c029.mp4%22%2C%22download%22%3Afalse%2C%22__spacing%22%3A%22both%22%2C%22id%22%3A%22KZC4C%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22video%22%7D#KZC4C)
---

<a name="F2lel"></a>
# 项目文件
[CoinFlip.zip](https://www.yuque.com/attachments/yuque/0/2024/zip/27393008/1705298240576-f9e842a3-1151-48e6-893d-3c73b04df3b7.zip)
