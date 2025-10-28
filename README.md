实验1：Android界面组件实验 实验信息 课程名称：移动应用开发

实验编号：实验1

实验名称：Android界面组件实践

学号：121052023045

姓名：林健

实验日期：2025.10.15

实验目标 掌握Android ListView信息发送用法、自定义布局的AlertDialog用法、XML定义菜单和上下文操作模式(ActionMode)的上下文菜单的使用方法

实验环境 环境组件 版本信息 开发工具 Android Studio Narwhal 3,Gradel 8.13 目标API API 21 开发语言 Java 项目包名com.example.myapplication

注意：本实验（实验一）核心代码在该仓库的“app”

一、项目设计思路

核心目标
创建一个最基础的Android应用程序，验证开发环境配置的正确性，掌握Android应用的基本结构和运行原理，为后续复杂应用开发奠定基础。

主要功能模块
应用启动：显示基本的欢迎界面

文本展示：在屏幕中央显示"Hello World!"文本

基础布局：使用最简单的布局容器

资源配置：基本的字符串和布局资源管理

用户需求分析
开发者需要验证Android开发环境是否正确配置

初学者希望通过简单项目理解Android应用的基本结构

用户期望看到应用能够正常安装和运行

项目应提供清晰的代码示例和学习起点

技术选型与实现
开发环境：Android Studio

编程语言：Java/Kotlin

构建工具：Gradle

目标平台：Android 5.0 (API 21) 及以上

二、项目功能实现

1. 主Activity实现
功能描述：作为应用的唯一界面，负责显示"Hello World"文本，是Android应用的入口点。

实现思路：

继承AppCompatActivity类

在onCreate方法中设置布局文件

通过布局文件定义界面显示内容

核心代码：

package com.example.myapplication;

import android.os.Bundle;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
    }
}
代码解析：

onCreate(): Activity生命周期方法，在Activity创建时调用

setContentView(): 设置Activity要显示的布局文件

R.layout.activity_main: 引用res/layout/activity_main.xml布局资源

2. 布局文件设计
功能描述：定义应用界面的视觉结构，使用约束布局确保文本在屏幕中央显示。

实现思路：

使用ConstraintLayout作为根布局

添加TextView控件显示"Hello World"文本

设置约束条件使文本居中显示

核心代码：

xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
布局解析：

ConstraintLayout: 灵活的布局容器，通过约束定位子视图

TextView: 文本显示控件

layout_constraint*: 约束条件，使文本在父容器中居中

textSize="24sp": 设置字体大小

textStyle="bold": 设置文字样式为粗体

3. 字符串资源管理
   
功能描述：将文本内容分离到资源文件中，便于国际化和管理。

实现思路：

在res/values/strings.xml中定义字符串资源

在布局文件中引用字符串资源

核心代码：

xml
<resources>
    <string name="app_name">Hello World</string>
    <string name="hello_world">Hello World!</string>
</resources>

4. 应用清单配置
   
功能描述：定义应用的基本信息、权限要求和入口Activity。

实现思路：

配置应用包名、图标和主题

声明MainActivity为启动Activity

设置必要的Intent过滤器

核心代码：

xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.MyApplication">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
清单解析：

package: 应用的唯一标识符

android:icon: 应用图标

android:label: 应用显示名称

android:theme: 应用主题样式

MAIN和LAUNCHER: 标识Activity为应用入口

三、关键技术细节
1. 项目结构分析
text
app/
├── src/main/
│   ├── java/com/example/helloworld/
│   │   └── MainActivity.java
│   ├── res/
│   │   ├── layout/
│   │   │   └── activity_main.xml
│   │   ├── values/
│   │   │   └── strings.xml
│   │   └── mipmap-*/
│   └── AndroidManifest.xml
└── build.gradle
2. Gradle配置
功能描述：定义项目的构建配置、依赖关系和编译选项。

核心配置：

gradle
android {
    compileSdk 33
    
    defaultConfig {
        applicationId "com.example.helloworld"
        minSdk 21
        targetSdk 33
        versionCode 1
        versionName "1.0"
    }
    
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
}

dependencies {
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
}
3. 资源文件说明
mipmap/: 应用图标资源，不同分辨率适配

values/: 字符串、颜色、样式等资源定义

layout/: 界面布局文件

drawable/: 图形和图片资源

四、项目亮点与扩展方向
1. 项目亮点
极简设计：代码量少，结构清晰，易于理解

标准规范：遵循Android开发最佳实践

环境验证：有效验证开发环境配置

学习基础：为复杂应用开发提供坚实基础

2. 核心概念掌握
通过此项目，开发者可以掌握：

Activity生命周期：理解onCreate等关键方法

布局系统：掌握XML布局文件的基本用法

资源管理：了解Android资源系统的组织结构

构建流程：熟悉Gradle构建过程

3. 学习路径建议
环境搭建：成功运行Hello World项目

界面学习：掌握各种布局和控件使用方法

交互实现：学习事件处理和用户输入

数据管理：掌握本地存储和网络请求

高级特性：学习多媒体、传感器等高级功能

4. 故障排除指南
常见问题及解决方案：

构建失败：检查Gradle版本和依赖配置

安装失败：确认设备USB调试已开启

运行崩溃：查看Logcat错误日志

界面异常：检查布局文件和资源引用

代码原址:https://github.com/L-part05/android-homework
