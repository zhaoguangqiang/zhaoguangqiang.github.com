---
layout: post
title: 杂项设备驱动杂记
discription: 
tags: linux
---
  
杂项设备：也是属于字符设备的范畴，其主设备号都为10，有利于节省系统资源，如看门狗  
	杂项设备：填充file_operations--->填充miscdevice--->misc_register设备注册进内核，自动生成设备节点  
		需要：次设备号，设备名，file_operations  
			GNU C 语法  
			//定义并初始化  
			.minor = 10;  
			minor : 10；  
			__init把代码放到固定的段中，只在初始化执行一次，使用完了就可以释放了  
	字符设备：填充file_operations--->register_chrdev()--->class_create()---->device_create()  
		需要：file_operations 主设备号 次设备号 设备名  
cdev：  
	在字符设备中：register_chrdev通常主设备号注册后，从设备号0~255全部被占用，无法另行注册，浪费资源  
		register_chrdev工作：让内核认识，注册进内核，让用户认识，设置设备节点  
	所以讲register_chrdev分解为(1)cdev:定义，初始化，注册(2)设备号：申请  
		注册流程：  
			申请设备号：dev_t 前十位主设备号，后22位从设备号  
			添加cdev  
		注销流程：  
			删除添加cdev  
			注销设备号  
	  
platform总线：几乎存在于每个驱动中  
input子系统：做输入设备，如鼠标，键盘，触摸屏  



















