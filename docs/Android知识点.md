## Android 的布局

Android 是通过容器的布局属性来管理子控件的位置关系，布局过程就是把界面上的所有的控件，根据他们的间距的大小，摆放在正确的位置

- 线性布局：LinearLayout

- 相对布局：RelativeLayout

- 帧布局：FrameLayout

- 绝对布局：AbsoluteLayout

- 表格布局：TableLayout

- 网格布局：GirdLayout

- 约束布局：ConstraintLayout

## Android 四大组件

- activity：与用户交互的可视化界面

- service：实现程序后台运行的解决方案，比如 qq 音乐的音乐在后台运行，没有界面

- content provide：内容提供者，提供程序所需要的数据，比如？提供数据库？

- broadcast receiver：广播接收器，监听外部事件的到来（比如来电）

## Android 常用的控件

- TextView：文本控件

- EditText：可编辑文本控件

- Button：按钮

- ImageButton：图标按钮

- ToggleButton:开关按钮

- ImageView：图片控件

- CheckBox：复选框控件

- RadioButton：单选框控件

## 控件知识

- dom：Document Object Model 文档对象模型

- dom 应用：最早应用于 html 和 js 的交互，用户表示界的控件层级，界面的结构化描述，常见的格式为 html、xml。核心元素为节点和属性

- xpath：xml 路径语言，用于 xml 中的节点定位

- Android 的应用层级结构是定制的 xml

- app source 类似于 dom，表示 app 的层级，表示界面里面所有的控件数的结构

- 每个控件都有它的属性（resourceid、xpath、aid），没有 css 属性

## 配置 adb 环境变量

1. 安装Android Studio

2. 获取 adb 路径
   打开Android Studio软件，点击File→Project Structure，点击SDK Location，Android SDK location下面一栏即adb的地址，复制此地址，粘贴到此电脑的地址栏，然后打开platform-tools，此时地址栏中即adb.exe的地址。

3. 配置 adb 环境变量
   依次点击环境变量→系统变量下的新建按钮。变量名填入ANDROID_HOME，变量值填入adb.exe的上一级目录地址，即C:\Users\Administrator\AppData\Local\Android\Sdk。最后点击确定。
   点击系统变量中的Path，点击编辑，点击新建，输入%ANDROID_HOME%\platform-tools，然后点击确定即可。至此环境变量配置完毕。
   在移动端测试的过程中，经常会用到一个工具uiautomatorviewer，它位于%ANDROID_HOME%\tools\bin，为了方便的调用这个工具，我们也需要将%ANDROID_HOME%\tools\bin添加至环境变量中。

4. 验证
   cmd中输入adb，进行验证。

## adb 常用命令

### 启动adb服务

```
adb start-server
```

### 终止adb服务

```
adb kill-server
```

### 查看连接计算机的设备

```
adb devices
```

### 连接夜神模拟器

```
adb connect 127.0.0.1:62001
```

### 登录设备的shell模式

```
adb shell
```

### 安装 apk

```
adb install <apkfile> //比如：adb install baidu.apk
```

### 保留数据和缓存文件，重新安装apk

```
adb install -r <apkfile> //比如：adb install -r baidu.apk

```

### 卸载APK(可使用adb shell "dumpsys activity | grep \"mFocusedApp\""命令查看前台应用包名后，使用包名进行卸载)

```
adb uninstall <package> //比如：adb uninstall com.baidu.search
```

### 卸载app但保留数据和缓存文件

```
adb uninstall -k <package> //比如：adb uninstall -k com.baidu.search
```

### 清除应用的数据和缓存

```
adb shell pm clear <package_name>
```

### 使用adb shell指令来查看当前栈顶的Activity(查看前台应用包名)

```
adb shell "dumpsys activity | grep \"mFocusedApp\""
```

### 从本地复制文件到设备

```
adb push <local> <remote>
```

### 从设备复制文件到本地

```
adb pull <remote>  <local>
```

### 启动应用

```
adb shell am start -n <package_name>/<activity_class_name>
```

### 列出所有包名

```
adb shell pm list packages
```

### 列出系统包名

```
adb shell pm list packages -s
```

### 列出第三方包名

```
adb shell pm list packages -3
```

### 打印日志

```
adb logcat
```

### 重启机器

```
adb reboot
```

### 查看设备cpu和内存占用情况

```
adb shell top
```

### 查看进程列表

```
adb shell ps
```

### 有多台设备连接时，定向操作的命令

```
adb -s deviceName <command> //比如：adb -s 127.0.0.1:62001 install Chrome.apk
```