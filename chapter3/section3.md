# 第三节 创建新的GUI客户端

## 1、范例程序说明

这个GUI程序是一个最简单的单界面程序，里面使用了jgoodies的Layout 、swing的JTable、IntelliJ的JForm。代码下载地址： [http:\/\/222.44.18.140\/svn\/pthink\/product\/PthinkCloudApp\/02.example\/02.client\/ExampleApplication](http://222.44.18.140/svn/pthink/product/PthinkCloudApp/02.example/02.client/ExampleApplication) 

界面如下：

![](/assets/05.png)

也引入了ClientAPI。工程创建方式基本雷同，但是pom.xml当中引入了更多的UI控件，便于编译和运行。

## 2、系统开发步骤

### A、新建一个工程

### B、新建一个GUI Form

Layout可以选择jgoodies或intellij

### C、为Form加入需要的UI组件

修改主panel的名字为mainpanel

### D、为控件加入相应事件

### E、为main方法加入执行方法

```java
private static JFrame _FrameMain;
private static ObjectPrx ICE_Connection = IceTradeUtil.getConnect(ConfigUtil.getInstance().getPropConfig().getStringArray("servers"));

public static void main(String[] args) { 
_FrameMain = new JFrame("GuiDemo"); 
_FrameMain.setContentPane(new GuiDemo().mainpanel); 
_FrameMain.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE); 
_FrameMain.setLocationRelativeTo(null); 
_FrameMain.setExtendedState(JFrame.MAXIMIZED_BOTH); 
int width = Toolkit.getDefaultToolkit().getScreenSize().width; //得到当前屏幕分辨率的高 
int height = Toolkit.getDefaultToolkit().getScreenSize().height;//得到当前屏幕分辨率的宽 
_FrameMain.setSize(width / 2, height / 2);//设置大小 
_FrameMain.setLocation((width - _FrameMain.getWidth()) / 2, (height - _FrameMain.getHeight()) / 2); //设置窗体居中显示 
_FrameMain.setIconImage(new ImageIcon("app.ico").getImage()); 
_FrameMain.pack(); 
_FrameMain.setVisible(true);}

```

