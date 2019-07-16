1. 被鎖定表察看
> SELECT 
> ORACLE_USERNAME, OS_USER_NAME, LOCKED_MODE, 
> OWNER, OBJECT_NAME, OBJECT_TYPE, CREATED, 
> LAST_DDL_TIME, TIMESTAMP, B.STATUS, MACHINE, 
> TERMINAL, PROGRAM 
> FROM V$LOCKED_OBJECT A, ALL_OBJECTS B, V$SESSION C
> WHERE A.OBJECT_ID = B.OBJECT_ID AND C.SID = A.SESSION_ID;
> 
> select oracle_username,os_user_name,locked_mode,object_name,owner,machine 
> from v$locked_object a,all_objects b,v$session c 
> where a.object_id=b.object_id and c.sid=a.session_id;


2. 数据转换
> TO_NUMBER()  
> TO_CHAR()  
> TO_NCHAR()  
> TO_DATE()  
> TO_CLOB()  
> TO_NCLOB()  
> CHARTOROWID()  
> ROWIDTOCHAR()  
> ROWIDTONCHAR()  
> HEXTORAW()  
> RAWTOHEX()  
> RAWTONHEX()  
> REFTOHEX()  
> SUBSTR(XXX, m, n)  

3. 试图
> 创建  
> CREATE VIEW视图名 AS ********  
> 修改视图  
> ALTER VIEW    需要有ALATER ANY TABLE权限  
> 删除视图  
> DROP VIEW 视图名   需要有DROP ANY VIEW权限  

4. DATE常用日期函数
> sysdate	()		当天  
> last_day()		本月最后一天  
> add_months(d,n)	d日期推n月  
> months_between(f,s)    日期f和s间相差月数  
> next_day(d,day)		后第一周指定day的日期  
> 例：next_day(sysdate,’Monday’)下周星期一的日期  

5. 日期格式及其输出
> Y或YY或YYY	年的最后一位、两位或三位  
> SYEAR或YEAR	年，SYEAR使公元前的年份前加一负号  
> Q		季度  
> MM		月份数  
> RM		月份数的罗马表示  
> Month		用9个字符长度表示的月份名  
> WW		当年第几周  
> W		本月第几周  
> DDD		当年第几天  
> DD		当月第几天  
> D		周内第几天  
> DY		周内第几天的缩写  
> HH或HH12	12进制小时数  
> HH24		24小时制  
> MI		分钟数（0~59）  
> SS		秒数（0~59）  

6. 备份数据库
>(1).  
>exp /@UTSTAR FILE=/ext/mnt/1001/BS/temp/TOSSBS04_1001_1.dmp TABLES=TOSSBS04_1001  QUERY=\"WHERE rownum\<=50000\"  
>imp /@UTSTAR FILE=/ext/mnt/1001/BS/temp/TOSSBS04_1001_3.dmp TABLES=TOSSBS04_1001 Ignore=y  
>(2).  
>exp utc404/utc404@UTSTAR file = ${HOME}/dmp/TOC0SE41.dmp tables = TOC0SE41  
>imp utc409/utc409@UTSTAR file = /home/apl/debug/BS/MAKE/src/bt/TESTDATA/TOSSBS02_1001.dmp TABLES=TOSSBS02_1001  ignore = y  

7. 配置文件
>D:\program\oracle81\network\ADMIN\tnsnames.ora  
>	SOUGOU_B =  
>  	(DESCRIPTION =  
>   	 (ADDRESS_LIST =  
>     	 (ADDRESS = (PROTOCOL = TCP)(HOST = 192.178.64.106)(PORT = 1521))  
>    	)  
>    	(CONNECT_DATA =  
>      	(SERVICE_NAME = UTSTAR2.TSTAR)  
>   	 )  
> 	 )  

8. 多对多更新（TABLE_B多条记录更新TABLE_A，B中一条对应多条A）  
>UPDATE TABLE_A A  SET  
>(  
>   A.AAA,  
>   A.BBB  
>)=  
>(  
>   SELECT  
>      C.AAA,  
>      C.BBB
>   FROM (  SELECT SUM(B.AAA),SUM(B.BBB) FROM TABLE_B B GROUP BY B.AAA,B.BBB ) C  
>   WHERE  
>       A.CCC = C.CCC  
>)  
>WHERE EXISTS(  
>    SELECT 1 FROM( SELECT SUM(D.AAA),SUM(D.BBB) FROM TABLE_B D GROUP BY D.AAA,D.BBB ) E  
>    WHERE  A.CCC = E.CCC  
>    )  

9. 对自己的外连接
>CREATE TABLE temp (  
>  product_type_code CHAR(7) NOT NULL primary key,  
>  mother_pt_code CHAR(7) constraint FK_temp_1 references temp(product_type_code) ON DELETE CASCADE/ON DELETE SET NULL)  
>注意:oracle只有ON DELETE 默认热RESTRICT,没有ON UPDATE  

10. 有效的Oracle列数据类型
>CHAR       固定长度的字符域，尾部使用空格填充    255字节  
>VARCHAR   变长字符域                            2KB  
>VARCHAR2  变长字符域                            2KB  
>LONG        变长字符数据                          2GB  
>NUMBER     变长数字数据                       Precision:1~38  
>(precision,scale)  
>DATE        公元前4712/1/1日到4712/12/31     4712/1/1  
>RAW         变长原始二进制数据                    255字节  
>LONG RAW   变长原始二进制数据                    2GB  
>RAWID       行内部地址变量类型                    6字节  
>ROWID/UROWID   存储每行地址信息  
11. LOB数据类型
>   BLOB      
>大二进制类型字段,用于将一些没有严格定义的大文件以二进制流的形势存储在数据库中,通常使用最多的是存储jpg文件和一些大文本, 4G,相当于LONG RAW，但比它更优。  
>   CLOB     
>全称为字符大型对象（Character Large Object)。它与LONG数据类型类似，只不过CLOB用于存储数据库中的大型单字节字符数据块，不支持宽度不等的字符集。可存储的最大大小为4G字节。  
>   NCLOB   
>基于国家语言字符集的NCLOB数据类型用于存储数据库中的固定宽度单字节或多字节字符的大型数据块，不支持宽度不等的字符集。可存储的最大大小为4G字节.  
>BFILE     
>当大型二进制对象的大小大与4G字节时，BFILE数据类型用于将其存储在数据库外的操作系统文件中；当其大小不足4G字节时，则将其存储在数据库内部的操作系统文件中，BFILE列存储文件定位程序，此定位程序指向服务器上的大型二进制文件。这些文件为只读。也许可以通过这种方式存储视频，此时那些无需通过数据库本身即可检索或保存数据的应用程序（如视频编辑器）  
