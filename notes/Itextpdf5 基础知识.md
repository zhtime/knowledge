# Itextpdf5 基础知识

业务背景：需要根据甲方提供的材料模板，生成对应的pdf文件（后台实现）

这里根据我遇到情况，记录当前需要的知识点，写的一些小Demo。

## 依赖引入

```xml
		<dependency>
			<groupId>com.itextpdf</groupId>
			<artifactId>itextpdf</artifactId>
			<version>5.5.10</version>
		</dependency>

		<dependency>
			<groupId>com.itextpdf</groupId>
			<artifactId>itext-asian</artifactId>
			<version>5.2.0</version>
		</dependency>
```



## 生成PDF基本步骤

```java
    public static  void main(String[] args) throws FileNotFoundException, DocumentException {
        //文件类,pdf存放的为止
        File file = new File("C:\\Users\\25246\\Desktop\\pdf文件.pdf");

        //创建文本对象
        Document document = new Document(PageSize.A4,60,60,60,40);

        //PdfWriter是iText编辑PDF文档的编辑器，那么就要指向新建的document，document为编辑对象
        //pdf输出对象 PdfWriter  
        PdfWriter.getInstance(document,new FileOutputStream(file));

        //打开document，表明向该文本加入内容
        document.open();

        Paragraph title = new Paragraph("PDF");
        title.setAlignment(Element.ALIGN_CENTER);
        title.setSpacingBefore(40f);
        document.add(title);

        // 关闭 document,内容到此为止
        document.close();

    }

}
```

![image-20210831160725505](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831160725505.png)

再看看内容

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831160748267.png" alt="image-20210831160748267" style="zoom:50%;" />

## 基础知识

### Document:文档对象

**构造方法：Document(Rectangle pageSize, float marginLeft, float marginRight, float marginTop, float marginBottom)**

指定**PDF的页面大小，页边距**。

```java
        Document document = new Document(PageSize.A4,60,60,60,40);
        //指定A4页面，左右边距为60，上下边距为40
```



当中几个比较实用的方法

1. **add()**：添加内容

   ```java
   		//创建一个段落，设置内容为PDF		
   		Paragraph title = new Paragraph("PDF");
           title.setAlignment(Element.ALIGN_CENTER);
           title.setSpacingBefore(40f);
   		//把段落加入到文档中
           document.add(title);
   ```

2. **newPage()**:新增一页

   ```java
           //添加新的一页
           document.newPage();
           document.add(new Paragraph("2PDF"));
           //显示空内容的页
           writer.setPageEmpty(false);
           //不会显示空内容的页
   //        writer.setPageEmpty(true);
   ```

    <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831162018900.png" alt="image-20210831162018900" style="zoom: 80%;" />

   

3. **getPageSize()页面大小**/**getPageNumber()-第几页**



### Rectangle 页面对象

**构造方法：Rectangle(float llx, float lly, float urx, float ury)**

补充:**llx 为Left ，lly 为Bottom,urx 为Right，ury 为Top**

下面通过一个例子来说明

```java
    public static  void main(String[] args) throws FileNotFoundException, DocumentException {

        // 页面的属性
        // 页面大小
        Rectangle tRectangle = new Rectangle(400,400,500,500);

        // 页面背景色
        tRectangle.setBackgroundColor(BaseColor.ORANGE);
        // 边框
        tRectangle.setBorder(1220);
        // 边框颜色
        tRectangle.setBorderColor(BaseColor.BLUE);
        // 边框宽度
        tRectangle.setBorderWidth(15.2f);

        //文件类,pdf存放的为止
        File file = new File("C:\\Users\\25246\\Desktop\\pdf文件.pdf");

        //创建文本对象
        Document document = new Document(tRectangle);

        //PdfWriter是iText编辑PDF文档的编辑器，那么就要指向新建的document，document为编辑对象
        PdfWriter writer = PdfWriter.getInstance(document,new FileOutputStream(file));

        //打开document，表明向该文本加入内容
        document.open();

        Paragraph title = new Paragraph("PDF");
        title.setAlignment(Element.ALIGN_CENTER);
        title.setSpacingBefore(40f);
        document.add(title);

        //添加新的一页
        document.newPage();
        document.add(new Paragraph("2PDF"));
        //显示空内容的页
        writer.setPageEmpty(false);
        //不会显示空内容的页
//        writer.setPageEmpty(true);


        // 关闭 document,内容到此为止
        document.close();java

    }
```

该方法用来设计页面属性

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831163514680.png" alt="image-20210831163514680" style="zoom:50%;" />



### BaseFont 支持中文

```java
        //新宋体
        //这里我是把字体放到项目里面来了
        String littleTitleFonts = ProjectIndustryPlanAnnualConfigServiceImpl.class.getResource("/fonts/newsimsun.TTF").toString();
        BaseFont littleTitleFont = BaseFont.createFont(littleTitleFonts,BaseFont.IDENTITY_H,BaseFont.NOT_EMBEDDED);
        //通过Font去设置字体的基本属性：大小，加粗等等
        Font twoFonts = new Font(littleTitleFont,14,Font.NORMAL);
        
//一般都是和段落连用，设置对应段落中字体
        Paragraph title = new Paragraph("这里的标题需要重制一下",twoFonts);
        title.setAlignment(Element.ALIGN_CENTER);
        title.setSpacingBefore(40f);
        document.add(title);
```

![image-20210831164233698](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831164233698.png)





### Element 接口

先看一个眼熟的

```java
title.setAlignment(Element.ALIGN_CENTER);
```

这个最常用的就是定义元素在位置

```
ALIGN_LEFT(居左)， ALIGN_CENTER(居中)、 ALIGN_RIGHT(巨中)， ALIGN_JUSTIFIED(两端对齐)
```



### **Paragraph 段落**

这个是我采用最多的，用来存放内容，特点: **新段落另起一行**

方法：

1. **add(Element)-添加**
2. **setSpacingBefore-设置上空白， setSpacingAfter(10f)-设置段落下空**
3. **setAlignment(Element.ALIGN_CENTER)-居中对齐；**
4. **setLeading(20f)-行间距**
5. **setIndentationLeft()-左缩进， setIndentationRight-右缩进， setFirstLineIndent-首行缩进**

```java
        Paragraph title = new Paragraph("这里的标题需要重制一下",twoFonts);
        title.setAlignment(Element.ALIGN_CENTER);
        title.setSpacingBefore(40f);
        document.add(title);


        Paragraph title1 = new Paragraph("本文整理汇总了Java中com.lowagie.text.Element.ALIGN_JUSTIFIED属性的典型用法代码示例。如果您正苦于以下问题：Java Element.ALIGN_JUSTIFIED属性的具体用法？Java Element.ALIGN_JUSTIFIED怎么用？" +
                "Java Element.ALIGN_JUSTIFIED使用的例子？那么恭喜您, 这里精选的属性代码示例或许可以为您提供帮助。",twoFonts);
        title1.setFirstLineIndent(20);
        title1.setLeading(12);
        document.add(title1);
```



### Phrase 短语对象

这个我一般配合着段落使用

方法：

1. **add(Element)-添加方法**
2. **add(Chunk.NEWLINE)-内部换行**

例子

```java
 Paragraph timeTitle = new Paragraph();
 timeTitle.add(new Phrase("二",eightFonts));
 timeTitle.add(new Phrase("〇",twoAnotherFonts));
 timeTitle.add(new Phrase("一九年",eightFonts));
 timeTitle.setAlignment(Element.ALIGN_CENTER);
 timeTitle.setSpacingBefore(20f);
```



### Image图片

插入图片

```java
        Image image = Image.getInstance("C:\\Users\\25246\\Desktop\\1.png");
		//居中
        image.setAlignment(Element.ALIGN_CENTER);
		//设置边框
        image.setBorder(Image.BOX);
		//边框颜色
        image.setBorderColor(BaseColor.BLACK);
		//旋转15°
        image.setRotationDegrees(15);
		//设置大小
        image.scalePercent(70,69);
        document.add(image);
```

![image-20210831170541971](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831170541971.png)



### Anchor（锚点、超链接）

```java
// Anchor超链接和锚点对象: internal and external links
Paragraph country = new Paragraph();
Anchor dest = new Anchor("我是锚点，也是超链接", twoFonts);
// 设置锚点的名字
dest.setName("Linked");
// 连接
dest.setReference("https://www.baidu.com");
country.add(dest);java
document.add(country);
```

| <img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831171051108.png" alt="image-20210831171051108" style="zoom:50%;" /> | ![](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210831171131710.png) |
| ------------------------------------------------------------ | ------------------------------------------------------------ |

下面才是用到的最多的，做布局整理的。



### Table、PdfPTable 表格对象

设置列数，这里设置两列

```java
PdfPTable table9 = new PdfPTable(2);
```

方法：

**setWidths(数组)-单元格宽度**

**setTotalWidth(300f)-表格的总宽度**

**setWidthPercentage(100)-表格的宽度百分比**

**setLockedWidth(true)-宽度锁定**

**setSpacingAfter(40f)-设置表格下面空白行**

 **setSpacingBefore(20f)-设置表格上面空白行**

**setPadding(2)-单元格的间隔 **

**setBackgroundColor(BaseColor.GREEN)-背景色**

**setBorderWidth(2)-边框宽度**

```java
PdfPTable table9 = new PdfPTable(2);
table9.setSplitLate(false);
//设置对其方式：居左
table9.setHorizontalAlignment(Element.ALIGN_LEFT);
//表格宽度百分比
table9.setWidthPercentage(100);
//表格总宽度和高度
table9.setTotalWidth(500f);
//单元格宽度，这里是按照两列表格
float[] cellsWidth = {0.35f,0.65f};
table9.setWidths(cellsWidth);
```

**addCell()-添加单元格**

这里把**addCell()**和 **PdfPCell**放在一起说，PdfPtable是创建表格的，PdfPCell就是用来往表格中添加内容的，基本上都放在一起使用的。



### **PdfPCell 单元格对象** 

单元格中一般都是和**段落**一起使用

```java
PdfPCell c19 = new PdfPCell(new Paragraph("测试申报",fourFonts));
```

来看看它的方法：

**setBackgroundColor(BaseColor.CYAN)-背景色**

**setMinimumHeight(30f)-最小高度**

**setFixedHeight(40f)-固定高度。表格的高度通过单元格高度完成**

**setBorder(Rectangle.NO_BORDER)-无边框**，**setBorderWidth(0)-无边框**，**setBorderColor(new BaseColor(255, 0, 0))-边框颜色**

**setHorizontalAlignment(Element.ALIGN_CENTER)-水平居中**

**setVerticalAlignment(Element.ALIGN_MIDDLE)-垂直居中。设置单元格内容的显示**

**setRowspan(2)-跨2行， setColspan(2)-跨2列**

```java
        PdfPTable table9 = new PdfPTable(2);
        //设置对其方式：居左
        table9.setHorizontalAlignment(Element.ALIGN_LEFT);
        //表格宽度百分比
        table9.setWidthPercentage(100);
        //表格总宽度和高度
        table9.setTotalWidth(500f);
        table9.setSplitLate(false);

        //单元格宽度，这里是按照两列表格
        float[] cellsWidth = {0.35f,0.65f};
        table9.setWidths(cellsWidth);

        //设置一个单元格，内容用段落
        PdfPCell c19 = new PdfPCell(new Paragraph("人生，特别是职场，你不强大，没有人和你讲道理，因为在有限的资源和缥缈的道理之间，多数人会毫不迟疑地选择前者。你会因为自己长得不帅，而拒绝喜欢你心仪的美女吗？讲道理，你根本配不上，" +
                "但你会和自己说，你人品好，你人靠谱，你人踏实。",twoFonts));
        //垂直居中
        c19.setHorizontalAlignment(Element.ALIGN_CENTER);
        c19.setVerticalAlignment(Element.ALIGN_MIDDLE);
        //设置额最小高度
        c19.setMinimumHeight(40f);
        PdfPCell c20 = new PdfPCell(new Paragraph("如何让自己强大起来？你先控制好自己的情绪，不要当情绪的奴隶。只有先冷静下来，你才会理性地选择下一步行动。\n" +
                "等到你可以不讲道理了，希望和你讲道理的人自然会多起来。到时候，你再选择不忘初心，也不迟。 作者：大隐者的深度影评",twoFonts));
        //垂直居中
        c20.setHorizontalAlignment(Element.ALIGN_CENTER);
        c20.setVerticalAlignment(Element.ALIGN_MIDDLE);
        //设置额最小高度
        c20.setMinimumHeight(40f);
        //添加到表格中
        table9.addCell(c19);
        table9.addCell(c20);

        document.add(table9);
```

![image-20210901161858802](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210901161858802.png)



这里要提一下：**table9.setSplitLate(false)**这个方法，有时候可能会遇到这样的情况：**使用itext的PdfPTable和PdfPCell生成PDF内容**

**当PdfPCell中的内容过长，页面剩余空白不足以填充时，PdfPCell的整格会自动换到下一页显示，导致上一页尾部一片空白，打印时尤其浪费**

通过上面那个方法，尽可能的让当前页能放多少放多少

网上找了一个非常经典的例子

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/20200106084907294.png" alt="img" style="zoom: 50%;" />





下面介绍几个核心的类，对于添加水印、合并PDF都是关键。

### PdfContentByte 层对象

操作PdfWriter对象

```java
//pdf的输出对象
PdfWriter wirter =  PdfWriter.getInstance(document,new FileOutputStream(file));
//拿到当前pdf页
PdfContentByte cb = writer.getDirectContent();
PdfContentByte cb = stamp.getUnderContent(1);// 拿到层,可以有页数
```



### PDF合并

在当前生成的pdf的基础上合并多个pdf为一个pdf

这里我只列出了部分代码

```java
		//文件类,pdf存放的为止
        File file = new File("C:\\Users\\25246\\Desktop\\pdf文件.pdf");

        //创建文本对象
        Document document = new Document(PageSize.A4);

		//使用PdfWriter实现PDF合并
		PdfWriter wirter =  PdfWriter.getInstance(document,new FileOutputStream(file));
		document.open();
		
		//读取PDF文档（ PdfReader ）
        //tPdfTemplateFile:需要传入pdf地址
        //PdfReader reader = new PdfReader(tPdfTemplateFile);// 模板
        PdfReader reader = new PdfReader("C:\\Users\\25246\\Desktop\\操作系统.pdf");// 模板
        //拿到生成pdf当前页
        PdfContentByte cb = writer.getDirectContentUnder();
        
       	//传入pdf的总页数
        int totalPage = reader.getNumberOfPages();
		//循环
        for (int j =1 ; j <= totalPage; j++){
            //创建新的一页
            document.newPage();
            // 从当前Pdf,获取第j页
            PdfImportedPage page = writer.getImportedPage(reader,j);
            //使用writer需要使用pdf的层,然后后添加  
            //0:距离左边界的距离
            //0：距离下边界的距离
            cb.addTemplate(page, 0, 0);
        }
        document.close();
```

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210901165256288.png" alt="image-20210901165256288" style="zoom: 33%;" />

合并成功



上面使用**PdfWriter** 来完成的，下面尝试使用**PdfCopy(PdfWriter的子类)**来完成

```java
        //文件类,pdf存放的为止
        File file = new File("C:\\Users\\25246\\Desktop\\pdf文件.pdf");

        //创建文本对象
        Document document = new Document(PageSize.A4);

		 //PdfCopy是PdfWriter子类
        PdfCopy copy = new PdfCopy(document,new FileOutputStream(file));
		document.open();
		
        
        //读取PDF文档（ PdfReader ）
        //tPdfTemplateFile:需要传入pdf地址
        PdfReader reader = new PdfReader("C:\\Users\\25246\\Desktop\\操作系统.pdf");// 模板

        //传入pdf的总页数
        int totalPage = reader.getNumberOfPages();
        //循环
        for (int j =1 ; j <= totalPage; j++){
            //创建新的一页
            document.newPage();
            // 从当前Pdf,获取第j页
            PdfImportedPage page = copy.getImportedPage(reader,j);
            copy.addPage(page);
        }

	 // 关闭 document,内容到此为止
        document.close();
```

这种方法我在使用的时候有个缺陷，在我原本创建的pdf中我使用这个方法合成其他pdf，最后的结果就是我合成的pdf中原本自己创建的内容没有合并。我没有找到解决的方法，我建议使用上面那种。这个方法适用于多个pdf合并，不适用在自己创建的pdf中合并其他pdf。



下面想说一下合并pdf的拓展，也就是合并pdf会出现的一些问题。

场景：**当前生成pdf时需要和其他的pdf进行合并，最后生成的pdf中会出现有些图片过大超过页面大小，有些发生了翻转问题**。



 PdfContentByte中 方法**addtemplate**的参数

```java
public void addTemplate(PdfTemplate template,
    double a, double b, double c, double d, double e, double f)
```

a，b，c，d，e和f是具有**三行三列**的**矩阵**的元素。

![enter image description here](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/Lq3Lb.png)

矩阵来表示二维系统中的转换

![enter image description here](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/6mkoA.png)

```
x' = a * x + c * y + e
y' = b * x + d * y + f

例如：
x' = 1 * x + 0 * y + e
y' = 0 * x + 1 * y + f
```

矩阵中第三列是固定的

**e和f值可用于平移。 a，b，c和d值可用于旋转和/或缩放操作。**这些参数展开如下

<img src="https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/SMeOc.jpg" alt="enter image description here" style="zoom: 80%;" />

之前使用的合并pdf方法是**addTemplate(template, e, f)**进行平移操作

```java
 			//e: 0 距离左边界的距离
            //f: 0 距离下边界的距离
            cb.addTemplate(template, 0, 0);
```

通过引入**a，b，c和d**，还可以**旋转和/或缩放template**

```java
public void addTemplate(PdfTemplate template,
    double a, double b, double c, double d, double e, double f)
```

但是这样的方法不利于多种情况下的判断，这里我才用**AffineTransform**类来对这六个参数进行重载，适用于多种条件下的判断



先来看看**AffineTransform类**

定义：表示2D仿射变换，其执行从2D坐标到其他2D坐标的线性映射，其保持线的“直线性”和“平行性”。 可以使用**平移，缩放，翻转，旋转和剪切**的序列来构造仿射变换。

这样的坐标变换可以使用一个 **3 x 3的矩阵**来表示，最后一列默认为 **[ 0 0 1 ]**。此矩阵将源坐标 (x,y) 变换为目标坐标 (x',y')，这一过程将坐标视为列向量，并用矩阵乘以坐标向

```
      [ x']   [  m00  m01  m02  ] [ x ]   [ m00x + m01y + m02 ]
      [ y'] = [  m10  m11  m12  ] [ y ] = [ m10x + m11y + m12 ]
      [ 1 ]   [   0    0    1   ] [ 1 ]   [         1         ] 
      
      x' = m00x + m01y + m02
      y' = m10x + m11y + m12
      m00:a
      m10:b
      m01:c
      m11:d
      m02:e
      m12:f
```

构造方法只说明我用到的

| AffineTransform(float m00, float m10, float m01, float m11, float m02, float m12) | 从6个浮点值构造新的 `AffineTransform` ，表示3x3变换矩阵的6个可指定条目。 |
| :----------------------------------------------------------- | ------------------------------------------------------------ |

方法

| concatenate(AffineTransform Tx) | 以最常用的方式将 `AffineTransform Tx`连接到此 `AffineTransform` Cx，以提供由 `Tx`映射到以前用户空间的新用户空间。 |
| :------------------------------ | ------------------------------------------------------------ |

参考：[关于itext：itext的含义是什么pdf pdfcontentbyte addtemplate的参数 | 码农家园 (codenong.com)](https://www.codenong.com/45930261/)

[AffineTransform - Java 11中文版 - API参考文档 (apiref.com)](https://www.apiref.com/java11-zh/java.desktop/java/awt/geom/AffineTransform.html)

[图形状态方法概述第 2 部分（iText 5） (what-when-how.com)](http://what-when-how.com/itext-5/overview-of-the-graphics-state-methods-part-2-itext-5/)

想知道具体如何计算的可以点击第三个参考链接



这里我是使用PdfWriter对象来完成pdf的合并

```java
//文件类,pdf存放的为止
    File file = new File("C:\\Users\\25246\\Desktop\\pdf文件.pdf");

    //创建文本对象
    Document document = new Document(PageSize.A4);

	//使用PdfWriter实现PDF合并
	PdfWriter wirter =  PdfWriter.getInstance(document,new FileOutputStream(file));
	document.open();
	
	//读取PDF文档（ PdfReader ）
    //tPdfTemplateFile:需要传入pdf地址
    //PdfReader reader = new PdfReader(tPdfTemplateFile);// 模板
    PdfReader reader = new PdfReader("C:\\Users\\25246\\Desktop\\操作系统.pdf");// 模板
    //拿到生成pdf当前页
    PdfContentByte cb = writer.getDirectContentUnder();
    
   	//传入pdf的总页数
    int totalPage = reader.getNumberOfPages();
	//循环
           for (int j =1 ; j <= totalPage; j++){
            document.newPage();
//           从当前Pdf,获取第j页
            PdfImportedPage page = writer.getImportedPage(reader,j);


            /**
             * reader:读取需要合成pdf的内容
             * Rectangle:页面对象
             * getPageSizeWithRotation：获取当前页面的大小
             * Rectangle中四个参数 ：llx 为Left ，lly 为Bottom,urx 为Right，ury 为Top
             */
            Rectangle pagesize = reader.getPageSizeWithRotation(j);
            //宽度：oWidth
            float oWidth = pagesize.getWidth();
            //高度：oHeight
            float oHeight = pagesize.getHeight();
            //规模 ：
            float scale = getScale(oWidth, oHeight);
            //新宽度
            float scaledWidth = oWidth * scale;
            //新高度
            //这里对合并pdf大小进行调整
            float scaledHeight = oHeight * scale;
            //获取当前pdf页面旋转度数
            int rotation = pagesize.getRotation();

            //pdf合并判断或旋转
               //6个参数对用a、b、c、d、e、f
            AffineTransform transform = new AffineTransform(scale, 0, 0, scale, 0, 0);
            switch (rotation) {
                //旋转度为0：不需要进行旋转
                case 0:
                    cb.addTemplate(page, transform);
                    break;
                //旋转度为90
                case 90:
                    AffineTransform rotate90 = new AffineTransform(0, -1f, 1f, 0, 0, scaledHeight);
                    rotate90.concatenate(transform);
                    cb.addTemplate(page, rotate90);
                    break;
                //旋转度为180
                case 180:
                    AffineTransform rotate180 = new AffineTransform(-1f, 0, 0, -1f, scaledWidth, scaledHeight);
                    rotate180.concatenate(transform);
                    cb.addTemplate(page, rotate180);
                    break;
                //旋转度为270
                case 270:
                    AffineTransform rotate270 = new AffineTransform(0, 1f, -1f, 0, scaledWidth, 0);
                    rotate270.concatenate(transform);
                    cb.addTemplate(page, rotate270);
                    break;
                default:
                    cb.addTemplate(page, scale, 0, 0, scale, 0, 0);
            }

        }

    document.close();
```



### 添加文字水印

**beginText()：开始，endText()结束**

**showTextAligned()这个方法有很多重载，可以添加方位，旋转等**

```java
public void ShowTextAligned(int alignment, String text, float x,float y, float rotation)
```

| 参数      | 参数说明：                                            |
| --------- | ----------------------------------------------------- |
| alignment | 左、右、居中(ALIGN_CENTER, ALIGN_RIGHT or ALIGN_LEFT) |
| text      | 要输出的文本                                          |
| x         | 文本输入的X坐标                                       |
| y         | 文本输入的Y坐标                                       |
| rotation  | 文本的旋转角度                                        |

```java
        BaseFont bfChinese = BaseFont.createFont("STSong-Light","UniGB-UCS2-H",BaseFont.NOT_EMBEDDED);
        PdfContentByte cb = writer.getDirectContent();
        cb.beginText();
        // 设置透明度
        PdfGState gs = new PdfGState();
        gs.setFillOpacity(0.2f);
        cb.setGState(gs);
        cb.setFontAndSize(bfChinese,180);
        cb.showTextAligned(Element.ALIGN_CENTER, "Hello World", 340, 410 , 60);
        cb.endText();
```

![image-20210902195233631](https://picturebedzhanghui.oss-cn-hangzhou.aliyuncs.com/img/image-20210902195233631.png)



以上就是我所遇到的一些问题。

这里看到了更加全面的，附上链接

[(13条消息) java itextpdf 5 基础知识_MY_MAIN的博客-CSDN博客](https://blog.csdn.net/qq_39181568/article/details/80003903)

