# 概述

### 面向框架编程

编写数据处理的规则 传递给框架 

用框架

- 读文档
- 装环境
- 写用例
- 写框架

## 什么是QT？

跨平台的C++图形用户界面应用程序框架

**QWidget --windows界面获取**

QTabWidget

**UI界面**

QLineEdit 多行编辑器

QTextEdit 单行编辑器

QGroupBox

QTableWidget

**QAbstracuButton**

QRadioButton

QPushButton

QCheckBox

**布局**

QHBoxLayout horizontal(水平布局)

QVBoxLayout vertical(垂直布局)

Ctrl + H 水平布局

Ctrl + I 垂直布局

**预览快捷键 alt + shift + r**

固定大小 setMaximumSize 和 MinimumSize(设置宽度、高度)相同，可以实现固定效果

# 创建项目

## **1. qmake vs CMake**

### **qmake**

- **定位**：Qt 官方原生的构建工具，专为 Qt 项目设计，语法简单，与 Qt 深度集成。
- 优点：
  - 自动处理 Qt 特有的元对象编译（MOC）、资源文件（QRC）、UI 文件（UIC）等。
  - **配置文件（`.pro`）简洁，适合快速开发 Qt 应用。**
- 缺点：
  - 功能相对局限，复杂项目配置可能不够灵活。
  - 非 Qt 项目支持较弱，逐渐被 CMake 取代。

### **CMake**

- **定位**：跨平台的通用构建系统，支持复杂项目结构和非 Qt 项目。
- 优点：
  - 高度灵活，支持多目录、多目标项目，可管理大型工程。
  - 生态强大，广泛用于 C++ 开源项目（如 VTK、OpenCV）。
  - Qt 官方推荐未来使用 CMake（Qt 6 逐步弱化 qmake）。
- 缺点：
  - 配置更复杂（需编写 `CMakeLists.txt`）。
  - **需要手动处理 Qt 模块的依赖（如 `find_package(Qt6 COMPONENTS Widgets)`）。**

## **2. MSVC vs MinGW**

### **MSVC（Microsoft Visual C++）**

- **定位**：**微软官方编译器，仅支持 Windows。**
- 优点：
  - 深度**集成 Windows SDK**，对 Win32 API 支持最佳。
  - **调试工具强大（与 Visual Studio 无缝协作）。**
  - 性能优化较好，尤其针对 Windows 平台。
- 缺点：
  - 仅限 Windows 平台。
  - 需要安装 Visual Studio（体积较大）。

### **MinGW（Minimalist GNU for Windows）**

- **定位**：**GCC 的 Windows 移植版，支持跨平台开发。**

- 优点：

  - 跨平台兼容性（代码可移植到 Linux/macOS）。
  - 轻量级，无需安装 Visual Studio。
  - 开源免费（MSVC 需商业许可）。

  缺点：

  - 对 Windows 特有 API 支持较弱。
  - 调试工具不如 MSVC 强大。
  - 性能可能略低于 MSVC。

## QMainWindow  VS QWidget

### **1. 功能定位**

- **QMainWindow**
  - **专为主窗口设计**，提供标准的应用程序主窗口框架，内置菜单栏、工具栏、状态栏、停靠窗口（Dock Widgets）和中央部件（Central Widget）的布局管理。
  - 适合作为应用程序的顶层窗口（如 IDE、文本编辑器等复杂界面）。
  - 默认有预设的布局结构，开发者只需填充内容即可。
- **QWidget**
  - **基础窗口类**，是所有用户界面对象的基类（包括 `QMainWindow`）。
  - 作为空白画布，需要手动实现布局和功能（如添加菜单栏需自定义）。
  - 适合简单对话框、子窗口或自定义控件。

------

### **2. 内置组件**

- QMainWindow

   包含以下预置区域：

  ```cpp
  setMenuBar(QMenuBar*)    // 菜单栏
  addToolBar(QToolBar*)    // 工具栏
  setStatusBar(QStatusBar*) // 状态栏
  setCentralWidget(QWidget*) // 中央部件
  addDockWidget(Qt::DockWidgetArea, QDockWidget*) // 停靠窗口
  ```

- **QWidget** **没有内置组件，所有界面元素需手动添加和布局。**

------

### **3. 使用场景**

- **QMainWindow**

  ```cpp
  QMainWindow window;
  window.setWindowTitle("Main Window");
  QTextEdit *editor = new QTextEdit(&window);
  window.setCentralWidget(editor); // 设置中央部件
  window.show();
  ```

  - 适用于需要标准界面结构的应用。

- **QWidget**

  ```cpp
  QWidget widget;
  QVBoxLayout *layout = new QVBoxLayout(&widget);
  layout->addWidget(new QPushButton("Button"));
  widget.setWindowTitle("Simple Widget");
  widget.show();
  ```

  - 适用于自定义弹窗、工具窗口或嵌入式部件。

------

### **4. 继承关系**

- `QMainWindow` 继承自 `QWidget`，因此拥有其所有功能，但扩展了主窗口特有的特性。

------

### **5. 何时选择？**

- 选择 **QMainWindow**：
  需要菜单、工具栏、状态栏等标准主窗口功能时。
- 选择 **QWidget**：
  开发简单窗口、自定义控件或子部件时。

tips:

​	如果需要将创建的类从QMainWindow变为QWidget 在未使用QMainWinow内置的控件的情况下可以将cpp中的继承父类改为QWidget，**若有ui文件，需要在外部修改其json代码中的QMainWidget变为QWidget**（在debug部分修改任何的ui文件，在编译时都会按照设计中的ui文件来修改代码）

# QT框架学习 



<img src="D:/Admin/Documents/GitHub/QTNote/QT%20notebook.assets/QT%E7%AC%AC%E4%B8%80%E7%AB%A0.png" alt="QT第一章" />



```C++
#include<iostream>
#include<QDebug>
QPushButton * btn(对象名) = new QPushButton (新的对象)
qDebug() << "输出语句";

btn.show();
btn.setParent(this);
btn.move(int x, int y);//x轴坐标 y轴坐标
Widget.Fixedresize(int w， int h);//宽度weight、高度height
```

            QCreater
            /
           /
        Qwidget
        /    \
       /     \
       btn    MyButton
  //创建的时候由上往下进行new操作
  //点击“×”释放内存的时候是由先从下往上进行delect操作

### tips:  

> 析构函数：
>   在程序释放内存时，会可以构建析构从而在释放内存时先执行析构的内容然后再去执行。
>   析构函数是特殊的类成员函数，简单来说，析构函数与构造函数的作用正好相反，它用来完成对象被删除前的一些清理工作，也就是专门的扫尾工作。如果构造函数打开了一个文件，最后不需要使用时文件就要被关闭，析构函数允许类自动完成类似清理工作，不必调用其他成员函数。
>  按照这个逻辑在执行析构的顺序应该是先执行btn的析构，因为btn是最先被释放的，然后执行Qwidget的析构。
>  逻辑没有错
>  但是在执行析构的时候会先寻找对象树的祖先，从根节点开始执行，所以在执行析构时的顺序时跟new对象的顺序是一样的
>  简而言之，在执行析构时会先执行Qwidget的析构，然后执行btn的析构函数。

 对象树

​                    QObeject
​                 /           |        \
​               /             |         \
​        QWidget   QWidget QWidget

  C++中规定了析构顺序应该按照其创建顺序的相反过程。那么问题来了，如果我们先创建了子对象，再创建的父对象，根据上述原理析构的时候先析构父对象，又因为Qt中的对象树自动析构原理，我们析构父对象会自动析构子对象。也就是说， 子对象此时就被析构了，然后代码继续执行，按照顺序还要再析构一次子对象，但是这时候已经是第二次调用 子对象的析构函数了，C++中不允许调用两次析构函数，因此，程序会崩溃。

##  打开外部程序

 QProcess

### WHAT?

The QProcess class is used to start external programs and to communicate with them

父类（Inherits）::QIODevice

### LineEdit信号系统书写方式

#### 信号写法

/* QProcess *myProcess = new QProcess(parent);
        myProcess->start(program, arguments);*/
    /*/windows/system32/notepad.exe/*/ //系统可以以这种形式启动起来
    QProcess *process = new  QProcess;
    QString startProgram = ui->cmdLineEdit->text();
    process->start(startProgram.trimmed()); //清楚空格

##  信号与槽

### What?

当按钮被做动作时（例如被点击时）会发出一个信号（singal）对应对象就会通过与他的connect函数进行连接 将处理这个信号的函数被称为槽函数(slot)。

### How?

**Connect(sender(this对象),signal(信号),receiver,slot)**

当找不到信号或者槽函数的时候 编译会出现错误 "XXXX" is not a member of QApplication

