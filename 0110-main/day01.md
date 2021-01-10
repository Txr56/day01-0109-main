## 一、Java环境的配置

### 1.1、JDK的安装
jdk包含了jre和java开发工具

java工具（javac、java、jps、jstack、native2ascii）

jre：运行程序
### 1.2、环境的配置
- path：路径（可执行文件的路径）

![path](../../../Desktop/PATH.png)
path的应用:如用annie下载腾讯视频、B站视频等

- classpath：class path（类路径）
  
- 需求：用java把导出到excel

1. 下载POI的jar包

使用下面的地址去下载
```
https://www.apache.org/dyn/closer.lua/poi/release/bin/poi-bin-4.1.2-20200217.zip
```
2. 写Java程序

```java
import java.io.FileOutputStream;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.LinkedList;
import java.util.List;

import org.apache.poi.hssf.usermodel.HSSFCell;
import org.apache.poi.hssf.usermodel.HSSFCellStyle;
import org.apache.poi.hssf.usermodel.HSSFRow;
import org.apache.poi.hssf.usermodel.HSSFSheet;
import org.apache.poi.hssf.usermodel.HSSFWorkbook;

/**
 * Description:
 * 作者：gu.weidong(Jack)
 * date:2018年9月27日
 * ProjectName:ExcelExport
 */
public class WriteExcel {
    public static void main(String[] args) throws ParseException {
        //创建一个HSSF,对应一个excel
        HSSFWorkbook workbook = new HSSFWorkbook();
        //在webbook中添加一个sheet,对应Excel文件中的sheet
        HSSFSheet sheet = workbook.createSheet("学生表");
        //在sheet中添加表头第0行,注意老版本poi对Excel的行数列数有限制short
        HSSFRow row = sheet.createRow((int) 0);
        //创建单元格，并设置值表头 设置表头居中
        HSSFCellStyle style = workbook.createCellStyle();

        HSSFCell cell = row.createCell(0);
        cell.setCellValue("学号");
        cell.setCellStyle(style);
        cell = row.createCell(1);
        cell.setCellValue("姓名");
        cell.setCellStyle(style);
        cell = row.createCell(2);
        cell.setCellValue("年龄");
        cell.setCellStyle(style);
        cell = row.createCell(3);
        cell.setCellValue("生日");
        cell.setCellStyle(style);

        //写入实体数据
        //      List list = DemoDaoImpl.getStudent();
        List list = new LinkedList<>();
        list.add(1);
        list.add(2);
        list.add(2);
        list.add(2);
        list.add(2);
        for (int i = 0; i < list.size(); i++) {
            row = sheet.createRow((int) i + 1);
            //     Student stu = (Student) list.get(i);
            //创建单元格，并设置值
            row.createCell(0).setCellValue(i);
            row.createCell(1).setCellValue("Jack");
            row.createCell(2).setCellValue(20);
            cell = row.createCell(3);
            cell.setCellValue(new SimpleDateFormat("yyyy-MM-dd").format(new Date()));
        }
        //将文件存到指定位置
        try {
            FileOutputStream fout = new FileOutputStream("E:/学生表.xls");
            workbook.write(fout);
            fout.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
java中很多第三方的应用都是以jar包的形式对外发布

## 二、变量、流程控制

### 2.1、标识符、数据类型
- 基本数据类型
```
整型(byte,short,int,long)

浮点型(float、double)

字符型(char)

布尔型(Ture、Flase)
```
- 引用类型
```  
类
  
接口
  
数组
```
### 2.2、声明变量和赋值

语法如下：

```
数据类型 变量名称
int a;
char c;
```
变量是一个容器（箱子）

byte age=22;

age=23;

### 2.3、流程控制

- 程序可以做某件事

- 程序在某个条件下做某件事
```
if ....else if...else
```
- 程序重复做某件事
```
for：明确循环次数

while：不明确循环次数
```
### 2.4、Java程序什么情况下算是结束

main线程结束，意味着jvm的退出

## 三、方法

### 3.1、方法的概念和语法

- 什么是方法？
```
能完成特定功能的代码的集合
```

- 如何定义方法

```
返回类型 方法名称(【参数1】,【参数2】.....){
    方法体
}
```
方法命名的依据？方法能完成什么功能

int c=abs(-5);
c是5

## 四、前四章综合案例

- 标识符
- 变量
- 流程控制
- 一维数组
- 二维数组
- 方法

编程的本质：调用方法


### 4.1、显示hero在屏幕上

- 知识点
```
声明变量
变量赋值
```

```java
class MainCanvas extends Canvas
{
	Image img;//变量的声明
	public MainCanvas(){
		try
		{
			img=Image.createImage("/sayo10.png");//变量赋值
		}
		catch (IOException e)
		{
			e.printStackTrace();
		}
	}
	public void paint(Graphics g){
		g.setColor(250,200,180);
		g.fillRect(0,0,getWidth(),getHeight());
		g.drawImage(img,100,100,0);
	}
}
```
### 4.2、让hero可以四个方向走动

- 声明hero的x坐标和y坐标
```java
int x,y;
```
- 给x和y赋初值

```java
x=100;
y=100;
```

- 把drawImage中的100和100替换为x和y
```java
g.drawImage(img,x,y,0);//第1个100是x坐标，第2个100是y坐标
```
- 在keyPressed中对x坐标和y坐标进行加减操作

```java
if(action==LEFT){
    System.out.println("向左走");
    x=x-1;
}
else if(action==RIGHT){
    System.out.println("向右走");
    x=x+1;
}
else if(action==UP){
    System.out.println("向上走");
    y=y-1;
}
else if(action==DOWN){
    System.out.println("向下走");
    y=y+1;
}
repaint();
```
### 4.3、让hero自然走动（两个图片来回切换）

- 声明变量
- 流程控制之if...else

思路分析

```
声明1个变量，我们来回改变该变量的值，不同的值显示不同的图片
例如：int f;
如果f是1，则显示sayo00.png
如果f是2，则显示sayo20.png
```

### 4.4、使用循环和一维数组

## 五、递归

### 5.1、递归的概念

### 5.2、递归出口

## 六、方法的结束

一个方法什么时候才算结束？
return调用就算方法结束了

