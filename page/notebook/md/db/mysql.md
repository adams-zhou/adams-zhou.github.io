1. 创建带外键的表
>      CREATE TABLE `数据库名`.`表名` (  
>       `字段1`,  
>       `字段2`,  
>      PRIMARY KEY(字段1),  
>      CONSTRAINT `FK_表名_1` FOREIGN KEY `FK_表名_1` (`字段2`)  
>        REFERENCES `表名` (`字段1`) ON DELETE RESTRICT  
>      )  
>      ENGINE = InnoDB;  
>      注:对自身的外键哦ON UPDATE CASCADE, ON UPDATE SET NULL,不起作用  

2. mysql数据隔离级别
>(1). Read uncommited  
>(2). Read commited  
>(3). Repeatable read  
>(4). Serializable  

3. 查看隔离级别
>select @@tx_isolation  

4. 事务支持
>InnoDB  支持事务  
>MyISAM  不支持事务  

6. 查看表磁盘 空间 
>select   
>	table_schema,  
>	concat(truncate(sum(data_length)/1024/1024, 2), 'MB') as data_size,  
>	concat(truncate(sum(index_length)/1024/1024, 2), 'MB') as index_size  
>from information_schema.tables  
>group by table_schema  
>order by sum(data_length) desc;  
