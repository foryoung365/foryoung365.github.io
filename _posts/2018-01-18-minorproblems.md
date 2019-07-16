---
layout: post
title: "小问题解决办法汇总"
description: "小问题解决办法汇总"
category: development
tags: [GameDevelopment]
---
{% include JB/setup %}

汇总一些平常碰到的小问题，方便查询。

## VS2015输入中文出现乱码，显示???的问题

* 删除所有的输入法 包括美式键盘，只留下常用的那个输入法，我的是搜狗，搞定。

## Flutter报错 Could not resolve all artifacts for configuration ':classpath'的问题
* 第一步：修改build.gradle,注释掉jcenter()，google()。使用阿里的镜像。原因是jcenter google库无法访问到导致的问题
pre. 
	buildscript {
		repositories {
		//google()
		//jcenter()
		maven { url 'https://maven.aliyun.com/repository/google' }
		maven { url 'https://maven.aliyun.com/repository/jcenter' }
		maven { url 'http://maven.aliyun.com/nexus/content/groups/public' }
	}

		dependencies {
			classpath 'com.android.tools.build:gradle:3.1.2'
		}
	}

	allprojects {
		repositories {
			//google()
			//jcenter()
			maven { url 'https://maven.aliyun.com/repository/google' }
			maven { url 'https://maven.aliyun.com/repository/jcenter' }
			maven { url 'http://maven.aliyun.com/nexus/content/groups/public' }
		}
	
* 第二步：找到fluttersdk目录 进入如下目录

Flutter/packages/flutter_tools/gradle
找到下 flutter.gradle文件 找如如下内容替换成和我一样的 把jcenter注释掉。
pre. 
	buildscript {
		repositories {
			//jcenter()
			//maven {
			// url 'https://dl.google.com/dl/android/maven2'
			//}
			maven{
			url 'https://maven.aliyun.com/repository/jcenter'
			}
			maven{
			url 'http://maven.aliyun.com/nexus/content/groups/public'
			}
		}
		dependencies {
			classpath 'com.android.tools.build:gradle:3.1.2'
		}
	}