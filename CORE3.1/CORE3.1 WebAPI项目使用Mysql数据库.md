# CORE3.1 WebAPI项目使用Mysql数据库

## 一、安装Nuget包

![image-20200609180052304](C:\Users\郭赋荣\AppData\Roaming\Typora\typora-user-images\image-20200609180052304.png)

Design和Tools 用于数据迁移

MySql.Data和Pomelo.EntityFrameworkCore.MySql 是MySql驱动

Z.EntityFramework.Plus.EFCore 是加强实体查询使用的。

## 二、定义模型

```c#
public class NewDbContext : DbContext
    {
        protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
        {
            optionsBuilder.UseMySql(@"server=[服务器IP地址];user=[用户名];database=[数据库名];port=[端口，默认是3306];password=[数据库密码];SslMode=None");
        }
        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Users>()
            modelBuilder.Entity<News>()
        }
        public DbSet<Users> Users { get; set; }
        public DbSet<News> News { get; set; }
    }
```

