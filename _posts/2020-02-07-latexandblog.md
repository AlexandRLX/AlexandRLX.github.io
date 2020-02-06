### xypic使用小提示
1. 原理
    在使用\xymatrix{} 后面那个大括号与内容的结尾在一行及其以内的距离才可以发挥作用.
	从同一目标发出的箭头,其箭头就要写在这个对象的后面.
	在同一水平线上的对象,就写在一行之内.
	尽量能够模块化的进行操作.
	\ar[r]^<<<<<< (<用来往右移后面的符号)
	\ar[r]^------ (-......左..........)

2. 例子
	$$
	\xymatrix{
	\Hom_{\C}(\ilim\alpha,\ilim\alpha) \ar[r] \ar[d] & \plim\Hom(\alpha,\ilim\alpha) \ar[d] \\
	\Hom(\ilim\alpha,X) \ar[r] & \plim\Hom(\alpha,X)	}
	$$ ((合乎文法的结尾要紧贴着结束内容))
   ![commutative diagram](https://raw.githubusercontent.com/AlexandRLX/AlexandRLX.github.io/master/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202020-02-07%20%E4%B8%8A%E5%8D%881.54.23.png)

### 如何在blog中插入图片
1. 将所选图片存储在电脑上,然后上传至github上
2. 在博文需要插入图片的地方 输入"![]()"其中[]中是对图片的描述是可以省略掉的.()中药输入图片的地址,也就是github上的位置.那也就是说如果我改变这个图片的位置,那我这片博客中的图片就会失效.真是伤脑筋呢.
