1. javascript内置函数、
> (1).alert(字符串)  
> (2).confirm(字符串)            true false  
> (3).eval(表达式)               计算  
> (4).parseFloat                 转float  
> (5).pareInt                    转int  
> (6).escape(Iso-Latin-1字符串)  
> (7).unescape(字符串)  
> (8).isNan(XX)                  不是数字  
	
2. 数组
	(1).旧版无数组，自制
	function make_array(index_num)
	{
		this.length = index_num
		for(var i = 0; i < index_num; i++)
			this[i] = 0
		return this
	}
	sung_arra = new make_array(4)
	
	(2).新版
	数组名=new Array(序号)

3. 数组对象的方法
	(1).Join()         将数组转换成字符串，以符号拼接
	(2).Reverse()
	(3).Sort()
	(4).slice(n, m)    截取数组中的一部分生成新的数组(n->m-1)
	(5).Concat()
	
4. typeof 关键字
	判断类型， number  string  boolean  object

5. screen对象   注小写screen
	availHeight
	availWidth
	colorDepth
	height
	pixelDepth
	width

6. Number对象
	Number(字符串)转数字，不是数字NaN
	
7. Math对象
	E        在自然对数下使用的Euler(欧拉)指数
	PI
	LN2
	LN10
	SQRT2    2的平方根
	SQRT1_2  1/2的平方根
	abs(x)
	acos(x)
	asin(x)
	atan(x)
	atan2(x)
	ceil(x)
	cos(x)
	exp(x)
	floor(x)
	log(x)
	max(x,y)
	min(x,y)
	pow(x,y)
	random()
	round(x)
	sin(x)
	sqrt(x)
	tan(x)

8. String对象
> 设定字体形状  
> big()  
> small()  
> blink()闪烁，Netsape支持  
> strike()  
> bold()  
> sub()  
> fixed()  
> sup()  
> fontsize(xx)  
> anchor("文字")  
> fontcolor("xx")  
> link("xx")  
> Italics()  
>   
> 字符串处理方法  
> charAt(索引)  
> charCodeAt(索引)  
> concat(字符串)  
> fromCharCode(编号1,...)  
> IndexOf(字符串)  
> lastIndexOf(字符串)  
> slice(索引1, 索引2)  
> split(分隔字符,个数)  
> substr(起始索引,长度)  
> substring(索引1, 索引2)  
> toLowerCase()  
> toUpperCase()  

9. JavaScript的事件
> onAort  
> onBlur  
> onChange  
> onClick  
> onDdlClick  
> onDragDrop  
> onErr  
> onFocus  
> onKeyDown  
> onKeyPress  
> onKeyUp  
> onLoad  
> onMouseMove  
> onMouseOut  
> onMouseOver  
> onMouseUp  
> onMove  
> onReset  
> onResize  
> onSelect  
> onUnload  

10. window对象的属性
> window.status="xxx"  
> 设置状态栏内字符串  
> window.defaultStatus="xxx"  

11. window对象的方法
> alert()  
> confirm()  
> prompt()  
> open()     window.open("new.html", "open_win1", "toolbar=yes, status=yes, resizeable=yes")  
> close()  
