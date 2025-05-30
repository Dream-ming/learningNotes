<a name="index">**Index**</a>
<a href="#0">MySQL笔记</a>  
&emsp;<a href="#1">基础内容</a>  
&emsp;&emsp;<a href="#2">1、MySQL体系结构</a>  
&emsp;&emsp;<a href="#3">2、数据类型：</a>  
&emsp;<a href="#4">SQL语句</a>  
&emsp;&emsp;<a href="#5">1、数据定义语言DDL，定义数据库对象（数据库、表、字段）</a>  
&emsp;&emsp;<a href="#6">2、数据操作语言DML，对表中的数据进行增删改</a>  
&emsp;&emsp;<a href="#7">3、数据查询语言DQL，查询表中的记录</a>  
&emsp;&emsp;<a href="#8">4、数据控制语言DCL，用来创建数据库用户、控制数据库访问权限</a>  
&emsp;<a href="#9">函数</a>  
&emsp;&emsp;<a href="#10">1、字符串函数</a>  
&emsp;&emsp;<a href="#11">2、数值函数</a>  
&emsp;&emsp;<a href="#12">3、日期函数</a>  
&emsp;&emsp;<a href="#13">4、流程控制函数</a>  
&emsp;&emsp;<a href="#14">5、聚合函数</a>  
&emsp;<a href="#15">约束</a>  
&emsp;&emsp;<a href="#16">1、常见的约束</a>  
<a href="#17">在插入数据时，不指定gender，则会默认为'男'</a>  
<a href="#18">当某一天插入失败（例如name重复），id仍然会被占用，插入下一条时，会跳过一个id</a>  
&emsp;&emsp;<a href="#19">2、外键</a>  
<a href="#20">建表时添加外键</a>  
<a href="#21">给表添加外键</a>  
<a href="#22">删除外键</a>  
&emsp;&emsp;<a href="#23">3、外键约束</a>  
&emsp;<a href="#24">多表查询</a>  
&emsp;&emsp;<a href="#25">1、内连接</a>  
&emsp;&emsp;<a href="#26">2、外连接</a>  
&emsp;&emsp;<a href="#27">3、自连接</a>  
&emsp;&emsp;<a href="#28">4、联合查询 union</a>  
&emsp;&emsp;<a href="#29">5、子查询</a>  
&emsp;<a href="#30">事务</a>  
&emsp;&emsp;<a href="#31">1、事务的四大特性</a>  
&emsp;&emsp;<a href="#32">2、操作</a>  
&emsp;&emsp;<a href="#33">3、并发事务问题</a>  
&emsp;&emsp;<a href="#34">4、事务隔离级别</a>  
&emsp;&emsp;<a href="#35">5、隔离级别操作</a>  
&emsp;<a href="#36">存储引擎</a>  
&emsp;&emsp;<a href="#37">1、操作</a>  
&emsp;&emsp;<a href="#38"> 2、存储引擎特点</a>  
&emsp;<a href="#39">索引</a>  
&emsp;&emsp;<a href="#40">1、索引结构</a>  
&emsp;&emsp;<a href="#41">2、索引分类</a>  
&emsp;&emsp;<a href="#42">3、索引语法</a>  
&emsp;&emsp;<a href="#43">4、查看 SQL 语句的效率</a>  
&emsp;&emsp;<a href="#44">5、索引失效的情况</a>  
&emsp;&emsp;<a href="#45">6、SQL 提示</a>  
&emsp;&emsp;<a href="#46">7、前缀索引</a>  
&emsp;<a href="#47">SQL 优化</a>  
&emsp;&emsp;<a href="#48">1、插入优化</a>  

# <a name="0">MySQL笔记</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

## <a name="1">基础内容</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="2">1、MySQL体系结构</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
* 连接层：处理数据库的连接、授权认证等
* 服务层：提供SQL接口、缓存查询、SQL的分析与优化
* 引擎层：负责数据的存储和提取，不同的引擎有不同的索引结构
* 存储层：将数据存储在文件系统之上，完成与存储引擎的交互

### <a name="3">2、数据类型：</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
* 数值类
    * 在关键字后面加 unsigned 使用无符号类型
    * tinyint、smallint、mediumint、int、bigint: 都是整数，分别占1、2、3、4、8个字节
        * tinyint unsigned：无符号1字节的整数 
    * float、double，浮点数
        * double(4, 1)：一共四位，小数占一位的浮点数类型
    * decimal，小数值

* 字符串类型
    * char、varchar(n): 定长(10)字符串，变长字符串
    * tinyblob、blob、mediumblob、longblob: 二进制文本，长度不同
        * 视频、音频、软件安装包是二进制文本，但是一般存放在单独的资源文件夹里，不放在数据库
    * tinytext、text、mediumtext、longtext: 不同长度的文本

* 日期时间类型
    * date: YYYY-MM-DD
    * time: HH:MM:SS
    * year: YYYY
    * datetime: YYYY-MM-DD HH:MM:SS


## <a name="4">SQL语句</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="5">1、数据定义语言DDL，定义数据库对象（数据库、表、字段）</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

1、数据库操作：   
* 查询当前存在的数据库
    * show databases;
* 查询数据库
    * select database();
* 创建数据库，中括号中的内容可有可无
    * create database [if not exists] 数据库名 [default charset 字符规则如utf8mb4] [collate 排序规则];
* 删除数据库
    * drop database [if exists] 数据库名;
* 使用数据库
    * use 数据库名;


2、表操作：   
* 查询当前数据库中所有的表
    * show tables;
* 查询表内容
    * desc 表名;
* 查询表的建表语句
    * show create table 表名;
* 创建一张表
    * create table 表名(字段1 类型 [comment 注释], 字段2 类型 [comment 注释]) [comment 表注释];
    * 表内不同字段用逗号分开，最后一个字段切记不要加逗号
    * 注释需要写comment关键字
* 修改表名
    * alter table 表名 rename to 新表名;
* 删除表
    * drop table [if exists] 表名;
* 删除表，并重新创建该表，相当于清空表操作
    * truncate table 表名;


3、字段操作：
* 添加字段
    * alter table 表名 add 字段名 类型(长度) [comment 注释] [约束];
* 仅修改字段的数据类型
    * alter table 表名 modify 字段名 新数据类型(长度);
* 修改字段名和字段类型
    * alter table 表名 change 旧字段名 新字段名 类型(长度) [comment 注释] [约束];
* 删除字段
    * alter table 表名 drop 字段名;


### <a name="6">2、数据操作语言DML，对表中的数据进行增删改</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

1、添加数据(insert)    
* 添加数据，只给几个字段赋值
   * insert into 表名 (字段1, 字段2, ...) values (值1, 值2, ...);
* 添加数据，给全部字段都赋值
   * insert into 表名 values (值1, 值2, ...);
* 批量添加数据
   * insert into 表名 (字段1, 字段2, ...) values (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);
   * insert into 表名 values (值1, 值2, ...), (值1, 值2, ...), (值1, 值2, ...);
* 如果插入的值是字符串和日期类型，要加单引号

2、修改数据(update)    
* 修改数据，中括号中的内容可以没有，如果不指定条件，则修改整张表的数据
   * update 表名 set 字段1 = 值1, 字段2 = 值2, ... [where 条件];

3、删除数据(delete)
* 删除数据，如果不指定条件，会删除整张表
* 无法删除某一个字段的内容，可以用update修改为null
   * delete from 表名 [where 条件];

### <a name="7">3、数据查询语言DQL，查询表中的记录</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

1、基本查询
* 查询多个字段
   * select 字段1, 字段2, 字段3, ... from 表名;
* 查询整张表
   * select * from 表名;
* 设置别名，as关键字可省略
   * select 字段1 [as 别名1], 字段2 [as 别名2], ... from 表名;
* 去除重复记录，添加关键字distinct
   * select distinct 字段 from 表名; 

2、条件查询
* 基础语法
   * select 字段 from 表名 where 条件;
* where 条件中的运算符
   * <, <=, >, >=, =
   * <>, !=   // 不等于
   * between ... and ...  // 在某一个范围之内，含左右值
   * in(...)   // 是列表中的值之一
   * like 占位符   // 模糊匹配(_匹配单个字符，%匹配任意个字符)
   * 例：select * from user where name = '__';   // 查询名字为两个字的数据
   * 例：select * from user where name = '%5';   // 查询名字最后一个字为'5'的数据
   * is null    // 是null
   * and, &&, or, ||, not, !   // 与或非
   * is not null   // 非null
* 使用聚合函数查询
   * select count(*) from user;   // 统计表中有几条数据
   * select count(name) from user;    // 统计表中有几条数据，如果 name 值为 null，则不会被统计
   * select avg(age) from user where name = '张三';   // 计算 name 为张三的人的平均年龄
   * select max(age) from user;
   * select sum(age) from user;

3、分组查询
* 基础语法
   * select 字段 from 表名 [where 条件] group by 分组字段名 [having 分组后过滤条件];
   * 先执行 where 筛选出符合条件的数据，再进行 having 的分组操作
   * where 不能使用聚合函数，having可以
* 例子
   * 按照年龄分组，第一列返回不同年龄，第二列统计每一个年龄的人数
      * select age, count(*) from user group by age;
   * 找出 name 为张三的人，按年龄分组，找出组成员>=3的组，返回年龄和年龄对应的人数，num是count(*)的别名
      * select age, count(*) num from user where name = '张三' group by age having num >= 3;

4、排序查询
* 基础语法
   * select 字段 from 表名 order by 字段1 acs, 字段2 desc...;
   * 先按第一个字段排序，相同的话再按第二个字段排序
   * acs升序(可省略)，desc降序
* 例子
   * 按照注册时间降序，年龄升序，给表排序
   * select * from user order by enterdata decs, age acs;
   

5、分页查询
* 基础语法
   * select 字段 from 表名 limit 起始索引, 查询记录数;
   * 起始索引从0开始，查询第一页可以不写起始索引
   * 每一页的起始索引 = (页码 - 1) * 每页的记录数
* 例子
   * 将表按每页十条数据分页，查询第一页和第二页
   * select * from user limit 10;   // 第一页，省略起始索引
   * select * from user limit 10, 10;   // 第二页

6、顺序问题
* 编写顺序
   * select - from - where - group by - having - order by - limit
* 执行顺序
   * from - where - group by - having - select - order by - limit
   * 先执行的取的别名可以给后执行的用，后执行的取的别名先执行的不能用
   * select 中取的别名给 where 用会报错

### <a name="8">4、数据控制语言DCL，用来创建数据库用户、控制数据库访问权限</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

1、查询用户
* use mysql;   // 在 mysql 的系统表中查询
* select * from user;

2、创建用户
* create user '用户名'@'主机名' identified by '密码';
* 用户名和密码自拟，主机名规定该用户可以在哪台主机上使用数据库
* 主机名：localhost - 当前主机，% - 所有主机

3、修改用户密码
* alter user '用户名'@'主机名' identified with mysql_native_password by '新密码';

4、删除用户
* drop user '用户名'@'主机名';

5、用户权限控制
* 权限
   * all, select, insert, update, delete, alter, drop, create
* 查询某用户的权限
   * show grants for '用户名'@'主机名';
* 授予权限
   * grant 权限 on 数据库名.表名 to '用户名'@'主机名';
* 撤销权限
   * revoke 权限 on 数据库名.表名 from '用户名'@'主机名';


## <a name="9">函数</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="10">1、字符串函数</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 拼接字符串
   * concat(s1, s2, ...)
* 转换成小写，大写
   * lower(s)
   * upper(s)
* 用字符串 pad 对 s 的左边进行填充，达到 n 个字符为止
   * lpad(s, n, pad)
* 对右边填充，直到达到 n 个字符为止
   * rpad(s, n, pad)
* 去除字符串头部和尾部的空格
   * trim(s)
* 返回字符串从 start 开始 len 长的子字符串
   * substring(s, start, len)
* 例子
   * 将用户的 uid 修改为五位数，不足的左边补零
      * update user set uid = lpad(uid, 5, '0');
   
### <a name="11">2、数值函数</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 向上取整
   * ceil(x)
* 向下取整
   * floor(x)
* 返回 x / y 的模
   * mod(x, y)
* 返回 0 ~ 1 内的随机数
   * rand()
* 四舍五入，保留 y 位小数
   * round(x, y)
* 例子
   * 生成一个六位数的随机验证码
      * select lpad(round(round() * 1000000, 0), 6, '0');

    
### <a name="12">3、日期函数</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 返回当前日期
   * curdate()
* 返回当前时间
   * curtime()
* 返回当前日期和时间
   * now()
* 获取指定 date 的年份
   * year(date)
* 获取指定 date 的月份
   * month(date)
* 获取指定 date 的日期
   * day(date)
* 返回一个 日期/时间 值加上一个时间间隔 expr 后的时间值
   * date_add(date, interval expr type)
   * date_add(now(), interval 70 day)   // 当前时间往后 70 天的时间
* 返回 起始时间data1 和 结束时间data2 之间的天数
   * datediff(date1, date2)   // date1 - date2，如果时间一更早，会返回负数
* 例子
   * 查询用户注册天数，按注册天数倒序排序
      * select uid, datediff(now(), entrydate) as 'entrydays' from user order by entrydays desc;


### <a name="13">4、流程控制函数</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 如果 val 为 true 返回 t，否则返回 f
   * if(val, t, f)
* 如果 val1 不为空，返回 val1，否则返回 value2
   * ifnull(val1, val2)
* 如果 val1 为 true 返回 res1，否则返回 default，其中 when 和 then 可以写多个
   * case when val1 then res1 ... else default end
* 如果 expr 的值等于 val1，返回 res1，否则返回 default 默认值
   * case expr when val1 then res1 ... else default end
* 例子
   * 查询用户的地址，如果是北京，显示'首都'，如果是上海，显示'魔都'，其他显示'其他
      * select name, (case addr when '北京' then '首都' when '上海' then '魔都' else '其他' end) from user;

### <a name="14">5、聚合函数</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* count - 统计数量
* max - 最大值
* min - 最小值
* avg - 平均值
* sum - 求和


## <a name="15">约束</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="16">1、常见的约束</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 主键       -   primary key
* 自动增长   - auto_increment
* 不为 null  - not null
* 唯一       - unique
* 检查条件    - check(条件)
* 设置默认值  - default val

* 例子
   * 创建一张表，id 为主键自动增长，name 不为空且唯一，age 在[0, 120]之间，gender 默认为 '男'
``` mysql
create table user(
    id int primary key auto_increment comment '主键',
    name varchar(10) not null unique comment '姓名',
    age int check( age > 0 && age <= 120) comment '年龄',
    gender char(1) default '男' comment '性别'
) comment '用户表';
# <a name="17">在插入数据时，不指定gender，则会默认为'男'</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
insert into user(name, age, gender) values ('tom', 12);
# <a name="18">当某一天插入失败（例如name重复），id仍然会被占用，插入下一条时，会跳过一个id</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
```

### <a name="19">2、外键</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

添加删除外键
``` mysql
# <a name="20">建表时添加外键</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
create table 表名(
    字段名 数据类型,
    [constraint] [外键名称] foreign key (外键字段名) references 主表 (主表列名)
);
# <a name="21">给表添加外键</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
alter table 表名 add constraint 外键名称 foreign key (外键字段名) references 主表 (主表列名);
# <a name="22">删除外键</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>
alter table 表名 drop foreign key 外键名称;
```

### <a name="23">3、外键约束</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* no action - 当父表中有删除/更新时，先检查是否有外键，如果有则不允许操作
* restrict - 同 no action
* cascade(级联) - 当父表中有删除/更新时，将外键对应的子表中的记录也更新
* set null - 当父表中有删除时，将子表的外键值修改为 null
* set default - 父表有变更时，子表将外键列设置成一个默认值(Innodb不支持)
* 添加外键约束
   * alter table 表名 add constraint 外键名称 foreign key (外键字段名) references 主表名(主表字段) on update cascade on delete set null;


## <a name="24">多表查询</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="25">1、内连接</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

只返回满足条件的行，不满足条件的行不显示

* 隐式内连接
   * 语法：select 字段1 字段2 from 表1 表2 where 条件;
   * 例：查询员工所在的部门，其中员工表记录了部门表的部门id
      * select emp.name dept.name from emp, dept where emp.dept_id = dept.id;
* 显示内连接
   * 语法：select 字段1 字段2 from 表1 [inner] join 表2 on 条件;   // inner 可省略
   * 例：select emp.name dept.name from emp [inner] join dept on emp.dept_id = dept.id;

### <a name="26">2、外连接</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

会返回左表或右表的所有行，外加交集

* 左连接
   * 取左表+两表交集
   * 语法：select 字段1 字段2 from 表1 left [outer] join 表2 on 条件;
   * 例：查询员工的所有信息，以及所在部门
      * select emp.* dept.id from emp left join dept on emp.dept_id = dept.id;
* 右连接
   * 取右表+两表交集
   * 语法：select 字段1 字段2 from 表1 right [outer] join 表2 on 条件;
   * 通常使用左连接

### <a name="27">3、自连接</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

将同一张表连接两次，取出内容

* 内连接
   * 语法：select 字段1 字段2 from 表名 别名1 表名 别名2 where 条件
   * 例：查询员工的领导名字，其中员工表中记录了自己的id，和领导的id
      * select a.name, b.name from emp a , emp b where a.managerid = b.id;
* 外连接
   * 语法：select 字段1 字段2 from 表名 别名1 left join 表名 别名2 on 条件
   * 例：上述查询，要求显示无领导的员工的内容
      * select a.name, b.name from emp a left join emp b on a.managerid = b.id;
   
### <a name="28">4、联合查询 union</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

将多次查询的结果上下拼接，要求列相同

* union all - 将查询结果全部拼在一起
* union - 将结果去重
* 例：查询用户为男，或者id小于100的用户的信息(若要去重，可以去掉关键字all，也可以直接一次查询条件解决)
   * select * from user where gender = '男' union all select * from user where id < 100;

### <a name="29">5、子查询</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 标量子查询
* 列子查询
* 行子查询
* 表子查询

## <a name="30">事务</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

事务是一组操作的集合，不可分割的工作单位，这些操作要么同时成功，要么同时失败

### <a name="31">1、事务的四大特性</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 原子性：事务是不可分割的最小操作单元，要么全部成功，要么全部失败
* 一致性：事务完成时，无论是否成功，必须使所有的数据都保持一致状态
* 隔离性：数据库提供隔离机制，保证事务在不受外部并发操作影响的独立环境下运行
* 持久性：事务一旦提交或回滚，对数据库中的数据的改变就是永久的，保留在磁盘中

### <a name="32">2、操作</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 查看事务提交方式
   * select @@autocommit;
* 设置事务为手动提交
   * set @@autocommit = 0;
* 在自动提交的环境下开启事务
   * start transaction;
   * begin;
* 提交事务
   * commit;
* 回滚事务
   * rollback;

### <a name="33">3、并发事务问题</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 脏读：一个事务读到另一个事务还没有提交的数据
   * A事务修改了数据，但未提交
   * B事务读到了A事务修改的数据
   * 若A事务回滚，则有问题
* 不可重复读：一个事务先后读取同一条记录，但两次读取的数据不同
   * A事务读取了一个记录
   * B事务修改了该记录，并提交
   * A事务再次读取该记录，得到的结果不一样
* 幻读：一个事务按照条件查询数据时，没有对应的数据行，但是在插入数据时，又发现有这行数据
   * A事务查询一个记录，发现没有该记录
   * B事务插入了该记录，并提交
   * A事务插入该记录，出现主键冲突
   * A事务再次查询该记录，但是已经解决了不可重复读问题，查询结果与上一次查询一致，仍然没有发现该记录

### <a name="34">4、事务隔离级别</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* read uncommitted - 读未提交
  * 不加锁读，直接读取内存中的最新版本数据（包括未提交的修改）
  * 加锁写，写操作时加排他锁，直到事务提交或回滚
  * 会出现脏读、不可重复读、幻读问题

* read committed - 读已提交
  * MVCC快照，每次 select 生成独立的 read view，读取已提交的最新版本
  * 写操作加行锁，无间隙锁，允许其他事务插入数据
  * 解决脏读问题，会出现不可重复读和幻读

* repeatable read - 可重复读
  * MVCC快照读
  * 写操作加间隙锁和行锁，防止其他事务插入新数据
  * 解决脏读和不可重复读，会出现幻读

* serializable - 串行化
  * 针对全表，读操作加共享锁，写操作加排他锁
  * 禁止快照读
  * 解决幻读问题，事务串行执行，无法并发，效率低


### <a name="35">5、隔离级别操作</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 查看隔离级别
   * select @@transaction_isolation;
* 设置事务隔离级别
   * set [session | global] transaction isolation level { 四个隔离级别的其中一个 };
   * session - 当前窗口
   * global - 所有环境
   * 四个隔离级别：read uncommitted, read committed, repeatable read, serializable


## <a name="36">存储引擎</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

引擎层：负责数据的存储和提取，不同的引擎有不同的索引结构

### <a name="37">1、操作</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 查看当前数据库支持的存储引擎
   * show engines;
* 建表时指定存储引擎
   * create table 表名 (字段) engine = innodb;

 ### <a name="38">2、存储引擎特点</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* InnoDB
   * 兼顾高可靠性和高性能，在 MySQL 5.5 之后，作为默认的存储引擎
   * DML操作遵循 ACID 模型，支持事务
   * 行级锁，提高并发访问性能
   * 支持外键约束
   * 每张表对应一个 .ibd 后缀的表空间文件，存储该表的结构、数据和索引
* MyISAM
   * MySQL早期的默认存储引擎
   * 不支持事务，不支持外键
   * 支持表锁、不支持行锁
   * 访问速度快
   * 每张表对应 .sdi .myd .myi 分别存储表结构、数据、索引
* Memory
   * 数据存储在内存中，受到硬件问题会丢失数据，只能用作临时表或缓存使用
   * 默认使用 hash 索引
   * 每张表对应 .sdi 存储表结构信息


## <a name="39">索引</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="40">1、索引结构</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 二叉树
   * 左子树的每一个节点都比根小，右子树的每一个节点都比根大
   * 顺序插入时，会形成一个链表，查询性能降低。大数据量情况下，层级较深，检索速度慢
* 红黑树
   *
   * 大数据量下，层级较深，检索速度慢
* B树
   * 多叉树结构，k阶的B树每个节点有 k - 1 个元素，k个指针，指向下一级。当插入后元素个数等于k，中间的元素插入上一级的元素中
   *  解决了层级深的问题。非叶子节点也会存储数据，导致键值减少，增加深度
* B+树
   * 在B树的基础上，中间元素插入上层元素的时候，保留一份在叶子节点上。并且叶子节点添加指针，形成单向链表
   * 解决深度的问题，非叶子节点仅存储索引，数据全部存放在叶子
* MySQL中的B+树
   * 在B+树的基础上，在相邻的叶子以及首尾叶子添加双向链表，形成一个双向循环链表
   * 在叶子中连续访问变得更方便
* hash
   * 通过哈希值，将数据存放在映射中。如果存在哈希冲突，在映射中使用链表存放在同一个位置
   * 只能比较等于，不支持范围查询，无法利用索引排序。不出现冲突的情况下，效率很高
   * memory引擎支持

### <a name="41">2、索引分类</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 主键索引 (primary)
   * 针对表中主键创建的索引
   * 默认自动创建，只能有一个
* 唯一索引 (unique)
   * 避免同一个表中某数据列中的值重复
   * 可以多个
* 常规索引
   * 快速定位特定数据
   * 可以多个
* 全文索引 (fulltext)
   * 查找文本中的关键词
   * 可以多个

* 聚簇索引
   * 将数据存储与索引放在一起，索引结构的叶子节点保存行数据
   * 必须有，且只能有一个
   * 选取规则：主键索引 - 第一个唯一索引 - InnoDB自动生成一个 rowid 隐藏索引
* 二级索引
   * 将数据与所有分开存储，索引结构的叶子节点关联的是对应的主键
   * 可以存在多个
* 回表查询
   * 通过二级索引找到主键，再通过聚簇索引找行数据

### <a name="42">3、索引语法</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 创建索引
   * create [unique | fulltext] index index_name on table_name (字段1, 字段2, ...);
   * 常规索引不需要中括号中指定类型
   * 为多个字段创建一个索引，称为联合索引
* 查看索引
   * show index from table_name;
* 删除索引
   * drop index index_name on 表名;

### <a name="43">4、查看 SQL 语句的效率</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 查看当前数据库每一种操作的频次
   * show global status like 'Com_______';
   * 七个下划线。返回每一种操作的数次
* slow_query_log 慢查询日志
   * show variables like 'slow_query_log';    查看慢查询日志是否开启
   * set global slow_query_log=ON;        启动慢查询日志（临时）
   * set long_query_time = 2;          设置慢查询阈值为 2s（临时）
   * 永久打开慢查询服务，需要打开mysql配置文件，修改内容
* profile 记录每一条 SQL 的耗时情况
   * select @@have_profiling;    查看是否支持工具
   * select @@profiling;    查看是否打开工具
   * set profiling = 1;    打开工具
   * show profiles;      查看每一条SQL的耗时情况
* 查看 SQL 的执行计划
   * 在 SQL 前面加上 explain 关键字
   * 会显示该 SQL 的具体执行情况，如使用的表，一步一步的执行顺序，查询数据的条数等信息

### <a name="44">5、索引失效的情况</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* 最左前缀法则
   * 如果使用了联合索引，索引了多列，在查询的时候必须要从最左边的索引开始使用
   * 假设对三列建立了索引，在查询时使用了不同的筛选
      * 如果筛选时对三列都设置了范围，则三个索引都生效
      * 如果对第一列和第三列设置范围，则只有第一列的索引生效
      * 如果对第二列和第三列设置范围，则三个索引都不生效
* 范围查询
   * 使用联合索引时，如果对某一列使用了大于或小于的范围查询，则右侧的列索引失效
* 运算操作
   * 在索引列时使用运算操作，索引会失效
* 字符串不加单引号
   * 在查询字符串的时候，where 中指定字符串内容，但是没有加单引号，能正确地的到结果，但是索引失效
* 模糊匹配
   * 模糊匹配时，对尾部模糊，索引生效。对头部模糊，索引失效
* or链接的条件
   * 用 or 链接查询的条件，如果有一个条件没有索引，则所有索引都失效
* 数据分布影响
   * 如果 MySQL 评估，使用索引比全表慢，则不使用索引

### <a name="45">6、SQL 提示</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

当某一列有单列索引和联合索引时，数据库会优先使用联合索引。可以通过 SQL 提示来指定使用的索引

* 推荐使用索引 (use)
   * select * from 表名 use index(推荐使用的索引名) where 条件;
* 不使用某索引 (ignore)
   * select * from 表名 ignore index(不使用的索引名) where 条件;
* 强制使用索引 (force)
   * select * from 表名 force index(索引名) where 条件;    

### <a name="46">7、前缀索引</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

当字段类型为字符串时，索引可能会很大，影响效率。可能只对一部分前缀建立索引

* 语法
   * create index idx_xxx on table_name(column(n));
   * column(n) 表示对字段的前 n 位建立索引

## <a name="47">SQL 优化</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

### <a name="48">1、插入优化</a><a style="float:right;text-decoration:none;" href="#index">[Top]</a>

* load 指令批量插入大数据
  * mysql --local-infile -u root -p;       // 链接数据库的时候加上参数 --local-infile
  * set global local_infile = 1;             // 开启从本地加载文件导入数据的参数
  * load data local infile 'path' into table '表名' fields terminated by ',' lines terminated by '\n';
    * 要载入的文件，字段之间用 ',' 分隔，行之间用 '\n' 分隔
    * 本地文件的格式需为：xxx1,yyy1,zzz1\n xxx2,yyy2,zzz2\n 
