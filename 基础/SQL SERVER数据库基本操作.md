## SQL SERVER

#### 存储过程

存储过程是一组予编译的SQL语句

优点：

- 允许模块化程序设计，就是说只需要创建一次过程，以后在程序中就可以调用该过程任意次。

- 允许更快执行，如果某操作需要执行大量SQL语句或重复执行，存储过程比SQL语句执行的要快。

- 减少网络流量，例如一个需要数百行的SQL代码的操作有一条执行语句完成，不需要在网络中发送数百行代码。

- 更好的安全机制，对于没有权限执行存储过程的用户，也可授权他们执行存储过程。

```mssql
create proc 存储过程名称
as
begin
	set nocount on;
	--sql语句
end
go	
```

#### 变量

```mssql
--1、变量名以@开头 select,set
declare @num int 
set @num=1
print @num

declare @num1 int =1
print @num1

declare @id int 
select @id from result where name=''
```

#### 事务

事务是指一个工作单元，它包含了一组数据操作命令，并且所有的命令作为一个整体一起向系统提交或撤消请求操作，即这组命令要么都执行，要么都不执行

```mssql
 begin transaction	--开启一个事务
 declare @error int=0	--定义变量 赋值
 --卖家，卖加的账户要加钱
 update AccountCompany set UserAccount = UserAccount+9000 where id=2
 set @error=@error+@@ERROR	--ERROR全局变量，获取错误的编号
 --买家，账户扣钱
 update AccountCompany set UserAccount = UserAccount-9000 where id=1
 set @error=@error+@@ERROR
 if @error<>0
	begin
		RollBack TRANSACTION --事务进行回滚
	end
  else
	begin
		COMMIT TRANSACTION --提交
	end
	
select * from AccountCompany
```

#### 触发器

优点：

1、触发器是自动的，当对表中的数据做了任何修改之后立即被激活

2、触发器可以通过数据库中相关表进行层叠修改

3、触发器可以强制限制，这些限制比用CHECK约束所定义的更复杂，与CHECK约束不同的是，触发器可以引用其他表中的列

##### 触发器的作用

触发器的主要作用就是其能够实现由主键和外键所不能保证的复杂参照完整性和数据的一致性，它能够对数据库中的相关表进行级联修改，提高比CHECK约束更复杂的的数据完整性，并自定义错误消息。触发器的主要作用主要有以下接个方面：

1. 强制数据库间的引用完整性
2. 级联修改数据库中所有相关的表，自动触发其它与之相关的操作
3. 跟踪变化，撤销或回滚违法操作，防止非法修改数据
4. 返回自定义的错误消息，约束无法返回信息，而触发器可以
5. 触发器可以调用更多的存储过程

触发器: 在对数据库数据进行操作（增加(insert)、修改(update)、删除(delete)）后，可以自动执行的操作

触发器分为两类：instead of 触发器 ，after(for)触发器。

　　instead of 触发器:在数据更新到数据库之前执行的操作

　　after(for)触发器：在数据更新到数据后再执行的操作

数据临时载体：inserted和deleted

　　inserted：存储操作中新增的或者更新的数据

　　deleted：存储操作中删除的数据

```sql
--Insert操作Instead of 触发器	在数据更新到数据库之前执行的操作
create trigger 触发器名称
	on 表名
	instead of insert --操作（增删改）
as
begin
	--需要执行的业务
end
--Insert操作After 触发器		在数据更新到数据后在执行的操作
create trigger 触发器名称
	on 表明
	After Insert
as
begin
	--需要执行的业务
end
--GO的意思是分批处理语句
```

#### 自定义函数

用户自定义函数的类型：

1、标量值函数（返回一个标量值）

2、表格值函数（内联表格值函数、多语句表值函数，返回一个结果集即返回多个值）

特点：内联表格值函数支持在WHERE子句中使用参数

```sql
--标量值函数
go
create function funName
(@strName nvarchar(50))
returns bit
as 
begin 
	declare @len bit
	if(len(@strName)>1)
	begin
		set @len=0
	end
	else
	begin
		set @len=1
	end

	return @len
end
go

select dbo.funName('张')
```

```sql
--内联表格值函数
go
create function fun1 (@id int)
returns table --返回一个表
as
	return select * from Lemon..Man where Id=@id;
	
go

select * from fun1(2)
```

```sql
--多语句表值函数
go
create function fun2
()
returns @tableName table(strname nvarchar)
as 
begin
	 insert @tableName select strname from @tableName
	 return 
end
```

#### OA工作流项目

- 工作流：一系列相互衔接、自动进行的业务活动或任务。

- OA工作流：建立于网络办公自动化基础上的事务行政审批，业务申请审批、公文、信息等的网上流转。它主要解决的是“使在多个参与者之间按照某种预定义的规则传递文档、信息或任务的过程自动进行，从而实现某个预期的业务目标，或者促使此目标的实现”。

- 不同于以往我们在仅仅进行增删改查（CRUD），我们还要对其进行  下订单--订单确认--财务收款--库管配货--运送  等等一系列操作。
- 工作流管理系统(Workflow Management System, WfMS)是一个软件系统，它完成工作量的定义和管理，并按照在系统中预先定义好的工作流规则进行工作流实例的执行。工作流管理系统不是企业的业务系统，而是为企业的业务系统的运行提供了一个软件的支撑环境。
  