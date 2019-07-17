1. java字符串
>//求字符串长度  
>void length(String s){  
>//基于char求字符串长度  
>System.out.printf("char len=%d\n", s.length());  
>//基于codepoint求字符串长度  
>System.out.printf("codepoint len=%d\n", s.codePointCount(0, s.length()));  
>}  
>
>//按文字循环
```java
void iterTest(String s){
	//基于char求字符串循环
	for(int charIndex=0; charIndex<s.length(); charIndex++){
		int c = s.charAt(charIndex);
		Sysem.out.printf("%x\n", c);
	}
	//基于codepoint求字符串循环
	for(int codeIndex=0; codeIndex<s.length();){
		int c = s.codePointAt(charIndex);
		Sysem.out.printf("%x\n", c);
		codeIndex += Character.charCount(c);
	}  
}
```

2. 判断数字
```java
if (Double.isNan(x))
```
3. n个数字中抽取k个数字
> n*(n-1)*(n-2)*...*(n-k+1)/1*2*3*...*k
```java
int lotteryOdds = 1;
for (int i=1; i<=k ;i++){
	lotteryOdds = ltteryOdds * (n - i + 1)/i;
}
```

4. UML开源工具
> ArgoUML(http://argouml.tigris.org)

5. 日期类
> GregorianCalendar
> DateFormataSymbols
> SimpleDateFormat

6. jar文件
> jar cvf file1 file2
> jar cfm **.jar manifest.mf **/**/**/*.class
> 更新已有的jar文件清单
> jar ufm **.jar manifest-additions.mf
> 
> 可执行jar文件
> jar cvfe **.jar **.**.**
> mf文件中添加Main-Class: **.**.**
> jar cvfm **.jr mainclass.mf

7. 切割字符串
split(String regex, int limit)
limit>0	表示数组可以切limit个，多出来的全部归到数组最后一位
limit=0	数组长度无限制，最后空字符省略
limit<0 数组长度无限制，不省略最后的空字符
split(String regex)=split(regex, 0)

8. 字符缓存
StringBuffer	多线程	xml解析，HTTP参数解析和封装
StringBuilder	单线程	如SQL语句的拼装，JSON封装等

9. 判断单词数量
Pattern pattern = Pattern.compile("\\b\\w+\\b");
Matcher matcher = pattern.matcher(str);
while(matcher.find()){
	***
}

10. 中文排序
String[] strs = {"张三","李四","王五"}；
Comparator c = Collator.getInstance(Local.CHINA);
Arrays.sort(strs, c);
for(String str : strs){
	System.out.println(str);
}

11. 偶数判断
i%2==1?"奇数":"偶数"	error
i%2==0?"偶数":"奇数"	correct

12. 银行家算法
RoundingMode.HALF_EVEN

13. 不要设置随机数的种子

14. 让工具类不可实例化
private 构造函数(){
	throw new Error("不要实例化我！");
}

15. 取第二大值
public static int getSecond(Integer[] data){
	List<Integer> dataList = Arrays.asList(data);
	TreeSet<Integer> ts = new TreeSet<Integer>(dataList);
	return ts.lower(ts.last());
}

16. List转Array
Arrays.asList(List);	基本类型的数组不能用
asList方法产生的List对象不可改变

17. 遍历效率
int sum = 0;

if (list instanceof RandomAccess){
	//随机存取如List
	for (int i=0, size=list.size();i<size;i++){
		sum += list.get(i);
	}
}else{//有序存取，如LinkedList
	for (int i : list){
		sum += i;
	}	
}

18. 频繁插入和删除时使用LinkedList

19. List.subList只是原列表的一个视图，所有的修改直接作用于原列表

20. 清除局部列表
list.subList(20,30).clear();

21. 排序
使用Comparator排序
class Employee implements Comparable<Employee>{
	....
	....
	publi int compartTo(Employee o){
		return new CompareToBuilder()
			.append(**,o.**)
			.append(**,o.**).toComparison()
	}
}

22. 使用binarySearch前先要排序

23. 集合操作
(1)并集
addAll(list)
(2)交集
retainAll(list)
(3)差集
removeAll(list)
(4)无重复的并集
list2.removeAll(list1)
list1.addAll(list2)

24. List交换
Collections.swap(list, i, j);

25. 打乱列表
Collections.shuffle(list)

26. 尽量让HashMap中的元素少量并简单

27. 多线程使用Vector或HashTable

28. Joda日期时间扩展包
(1)本地格式的日期时间
DateTime dt = new DataTime();
dt.dayofWeek().getAsText(Local.ENGLISTH);//英语星期几
dt.toLocalDate();//本地日期格式
dt.toString(DateTimeFormat.forPattern("yyyy年M月d日"));

(2)
DateTime dt = new DateTime();//DateTime是不可变类型
dt.plusHours(100).dayofWeek();//加100小时是星期几
dt.plusDays(100).toLocalDate();//加100天
dt.minusYears(10).dayofWeek().getAsText();//减10年
Hours.hourBetween(dt, new DataTime("2012-12-21")).getHours();//离2012-12-21几小时

//当前可变时间
MutableDateTime mdt = new MutableDateTime();
DateTime destDateTime = dt.plusYears(10);
while (mdt.isBefore(destDateTime)){
	mdt.addDays(1);
	if (mdt.getDayOfMonth()==13 && mdt.getDayOfWeek()==5){
		System.out.println("黑色星期五:" + mdt);
	}
}

(3)时区时间
DateTime dt = new DateTime();
dt.withZone(DateTimeZone.forID("Europe/London"));
dt.withZone(DateTimeZone.UTC);//标准时间

与JDK Date转换
DateTime dt = new DateTime();
Date jdkDate = dt.toDate();
dt = new DateTime(jkdDate);

29. 序列化sample
import java.io.*;
public class SerializationUitils{
	private static String File_NAME = "d:/temp/obj.bin";
	public static void writeObject(Serializable s){
		try{
			ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream(File_NAME));
			oos.writeObject(s);
			oos.close();
		}catch (Exception e){
			e.prinStackTrace();
		}
	}
	public static Object readObject(){
		try{
			ObjectInput input = new ObjectInputStream(new FileOutputStream(File_NAME));
			obj = input.readObject();
			input.close();
		}catch (Exception e){
			e.prinStackTrace();
		}
		return obj;
	}
}
需要序列化的类必须implements Serializable,并生成serialVersionUID

30. 利用序列化实现对象深层拷贝
import java.io.*;
public class CloneUtils{
	//拷贝对象必须实现序列接口
	public static <T exends Serializable>T clone(T obj){
		T clonedObj = null;
		try{
			ByteArrayOutputStream baos = new ByteArrayOutputStream ();
			ObjectOutputStream oos = new ObjectOutputStream(baos);
			oos.writeObject(obj);
			oos.close();
			
			ByteArrayInputStream bais = new ByteArrayInputStream(baos.toByteArray());
			ObjectInputStream ois = new ObjectInputStream(bais);
			clonedObj = (T)ois.readObject();
			ois.close();
		}catch (Exception e){
			e.printStackTrace();
		}
		return clonedObj;
	}
}

31. java调用JS
```java
ScriptEngine engine = new ScriptEngine Manager().getEngineByName("javascript");
Bindins bind = engine.createBindings();
bind.put("factor", 1);

engine.setBindings(bind, ScriptContext.ENGINE_SCOPE);
engin.eval(new FileReader("src/com/adams/callJs/model.js"));
if (engin instanceof Invocable){
	Invocable in = (Invocable)engine;
	Double result = (Double)in.invokeFunction("formula");
	System.out.println(result.intvalue());
}
model.js
function formula(var1, var2){
	return var1 + var2 - factor;
}
```
32. 本地化
native2ascii -encoding Shift-Jis XXX.properties XXXX.properties