1. 导入和导出
>bcp 数据库名.拥有人.tablename out "XXX.txt" -c -Jsjis -t"|" -UXXX -PXXX -SXXX -I XXX.ini  
>ini文件  
>[servename]  
>query=TCP, 域名, 端口名  
>  
>bcp 数据库名.拥有人.tablename in "XXX.txt" -c -Jsjis -Y -UXXX -PXXX -SXXX -I XXX.ini -f XXX.ctl  
>ctl文件是控制文件，列信息，另见baidu  
