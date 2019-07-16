
1. 启动服务
>cd D:\Program Files\PostgreSQL\9.4\bin  
>pg_ctl start -D "D:\Program Files\PostgreSQL\9.4\data"     得一直开着  

2. 注册服务
>cd D:\Program Files\PostgreSQL\9.4\bin  
>pg_ctl register -N PostgreSQL -D "D:\Program Files\PostgreSQL\9.4\data"  
>net start PostgreSQL  
>
>HEY_LOCAL_MACHINE -> SYSTEM -> ControlSet001 -> services -> postgresql  
	
3. 没试过，应该用
>sc create postgresql binpath= "D:\Program Files\PostgreSQL\9.4\bin\pg_ctl.exe" runservice -N "PostgreSQL" -D "D:\Program Files\PostgreSQL\9.4\data"  
>随便写点值，后面再去注册表改  
>cmd-regedit  
>HEY_LOCAL_MACHINE -> SYSTEM -> ControlSet001 -> services -> postgresql  
>ImagePath  -----  "D:\Program Files\PostgreSQL\9.4\bin\pg_ctl.exe" runservice -N "PostgreSQL" -D "D:\Program Files\PostgreSQL\9.4\data"  
>sc config postgresql start= auto  
>sc start postgresql   
>
>sc delete postgresql  
