---
title: php_shuzu
date: 2018-12-16 22:07:40
tags:
---
## 数组函数 对象

## 数组：
	定义一个数组：第一种$arr=array();或者第二种$arr =[];
	创建数组时添加元素：$arr=array('wang','133');

	数组分类：关联数组和索引数组：
	关联数组：
$arr1=[
'name'=>'wang',
'pass'=>'111'
];
## 索引数组：
$arr=array('wang','133');

## 索引数组添加元素：
$arr51[2] = '144';

## 关联数组添加内容：
$arr["fun"]='钓鱼';

## 混合关联数组和混合数组：
$arr =array(
'name'=>'wang',
18,
5 =>'hello'
);
	
## 数组可以放任何类型的数据
$arr6 =[fopen(),true,3.14,[123,455]];

## 数组长度计算：
echo count（$arr）;

echo sizeof($arr6);

## 数组中元素的排序：sort($arr)升序

$arr7 =[12,5,6,'12a'];
sort($arr7) ;

## 数组的输出：
索引数组：echo $arr7[0];
关联数组：echo $arr["name"];

用foreach($arr as $key=>$value){
		echo $key,$value;
		
## 用for ($i=0;$i<count（$arr）;$i++){
echo $arr[$i];
}

## 统计数组键个数array_count_value()
创建包含数组所有键名的新数组：array_keys()

数组指针：current()
销毁变量：unset（）
判断变量是否定义isset()
合并两个数组，一个组是键名，另一个为值array_combine()

		

## 函数	
函数名不区分大小写
function name(){
echo "yi";
}
echo "wang";
name();			//wangyi

## 函数中传入参数：
function b($a,$b){
	echo $a+$b;
}
b(123,456);   //579

## 函数返回值：
function b($a,$b){
$count=$a+$b;
return $count;
}
b(123,456);
$data=b(123,456);
echo $data;

## 随机数 rand（）
		
### 练习：	//参数1舒勇ARGV[1]获取，参数2使用ARGV[2]  参数传入后是string格式,获取随机从命令行输入的随机参数
function suiji($a,$b){
	$a= (int)$a;$b=(int)$b;

if ($a=="" || $b==""){
	print "请输入两个正整数";return;
}
else if ($a>$b){
	$rr=rand($a,$b);
}
else {
	$tmp=$b;
	$b=$a;
	$a=$tmp;
	$rr=rand($a,$b);
}echo $rr;
}
suiji($argv[1],$argv[2]);
	
## 面向对象：

class person{
public $name ='duan';
public $age=21;

function go(){
	echo $this->name .'is running';
}
}

$p1=new person();
$p1->name ='xu';
echo $p1->name;

$p2=new person();
$p2->name='cai';

## 构造函数：destruct 	
继承 class newperson extends person{}

方法覆盖:
		
## 全局变量：  
		$_GET;
		$_POST;
	