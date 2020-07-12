# U袋商城功能模块

# 一、商品管理

**商品列表**                            郭赋荣    GetProducts    需要分页

**添加新商品**                    张涛       AddProduct    

**商品分类、**                        张涛      ProductCategory  

**用户评论、**                        李传明    UserComment   增删

*商品回收站*                     

商品.批量上传、              

商品批量导出、                

商品自动上下架

**缺货登记、**        李传明    ShortSupply



### 商品分类表

`ProductCategory` 

| 字段          | 类型         | 是否可null | 约束 | 备注                         |
| ------------- | ------------ | ---------- | ---- | ---------------------------- |
| CategoryId    | int          |            | key  | 商品分类id                   |
| CategoryName  | nvarchar(10) |            |      | 商品分类名称                 |
| ParentId      | int          |            |      | 父级id                       |
| CategoryLevel | int          |            |      | 分类级别自动维护  SaveChange |

### 商品表

`Products

| 字段        | 类型         | 是否可null | 约束 | 备注     |
| ----------- | ------------ | ---------- | ---- | -------- |
| ProductId   | int          |            | key  | 商品id   |
| ProductName | nvarchar(50) |            |      | 商品名称 |
|             |              |            |      |          |
|             |              |            |      |          |



# 二、促销管理

**优惠券**              张涛    Coupon    增删改

团购活动、     

专题活动、

拼团活动、

**优惠活动、**      郭赋荣    PreferentialActivities

批发管理     



# 三、订单管理

**订单列表、**         李传明    OrderList

**订单查询、**        郭赋荣    OrderQuery

合并订单、       

订单打印、



**添加订单、 **       张涛      AddOrder

发货单列表、

退货单列表

## 订单管理表

|         列名         |    数据类型    | 允许Null值 | 约束条件 |             备注              |
| :------------------: | :------------: | :--------: | -------- | :---------------------------: |
|       OrderId        |      int       |   nonull   |          |           订单编号            |
|      CreateTime      |    datetime    |   nonull   |          |           创建时间            |
|     PaymentTime      |    datetime    |   nonull   |          |           付款时间            |
|       DealTime       |    datetime    |   nonull   |          |           成交时间            |
|     ProductName      | nvarchar(100)  |   nonull   |          |           商品名称            |
|     ProductPrice     |    decimal     |   nonull   |          |           商品总价            |
|       Freight        |    decimal     |   nonull   |          |             运费              |
|     RealPayMoney     |    decimal     |   nonull   |          |            实付款             |
|      StoreName       |  nvarchar(50)  |   nonull   |          |           店铺名称            |
|       StoreId        |      int       |   nonull   |          |            商品ID             |
|    PaymentMethod     |      int       |   nonull   |          |  付款方式1支付宝2微信3云闪付  |
|        Amount        |      int       |   nonull   |          |             数量              |
|        Coupon        |      int       |   nonull   |          |            优惠券             |
|        UserId        |      int       |   nonull   |          |            用户ID             |
|   ReceivingAddress   | nvarchar(100)  |   nonull   |          |           收货地址            |
|   ShippingAddress    | nvarchar(100)  |   nonull   |          |           发货地址            |
| LogisticsInformation | nvarchar(1000) |   nonull   |          |           物流信息            |
|     DeliveryTime     |    datetime    |   nonull   |          |           配送时间            |
|   0PurchaseSpecies   | nvarchar(100)  |   nonull   |          |         商品购买种类          |
|     Integration      |      int       |   nonull   |          |             积分              |
|     OrderStatus      |      int       |   nonull   |          | 订单状态1未支付2已支付3退货中 |
|   LogisticsStatus    |      int       |   nonull   |          |    物流状态1已发货2未发货     |
|    ProductPicture    |  varchar(50)   |   nonull   |          |           商品图片            |
|                      |                |            |          |                               |



# 四、广告管理

**广告列表、**         张涛      AdvertList

**广告位置**            张涛      AdvertPlace

# 五、报表统计

**流量分析、**                     郭赋荣  PV  

**客户统计**、                     郭赋荣    CustomCensus

**订单统计**、                     李传明    OrderCensus

**销售明细、**                    李传明    SalesDetails

搜索引擎、    

**销售排行、**                  张涛      SalesRank

访问购买率

# 六、平台公告

**新闻分类、**          张涛   NewCategory  

**新闻列表**、          张涛  NewList

文章自动发布、

在线调查

## 平台公告

|        列名         |    数据类型    | 允许空值 |   备注   |
| :-----------------: | :------------: | -------- | :------: |
|  AnnouncementTitle  | nvarchar(100)  |          | 公告标题 |
| AnnouncementContent | nvarchar(1000) |          | 公告内容 |
| AnnouncementSpecies |  nvarchar(50)  |          | 公告种类 |
|       StoreId       |      int       |          |  商品ID  |
|   AnnouncementId    |      int       |          |  公告ID  |



# 七、会员管理

**会员列表、**        李传明     MemberList

**添加会员**、       郭赋荣   AddMember

**会员等级、**       郭赋荣   MemberLevel

会员留言、       

**充值和提现申请、**   李传明

**资金管理**          李传明

# 八、权限管理

**管理员列表**           张涛  ManagerList

管理员日志、      

**角色管理、**          郭赋荣    RoleManage

办事处列表、



# 九、系统设置

**供货商列表**       李传明

商店设置、      李传明

会员注册项设置、      张涛    MemberRegister

支付方式、        李传明     

配送方式、     郭赋荣

邮件服务器设置、   

地区列表、

# 十、模块管理

模块选择、

设置模块、

库项目管理、

语言项编辑、

模块设置备份、

邮件模板

# 十一、数据库管理

数据库备份、

数据表优化

# 十二、短信管理

发送短信

# 十三、推荐管理

推荐设置、

分成管理

# 十四、邮件群发管理

关注管理、

邮件订阅管理、

杂志管理、

邮件列表管理



# **郭赋荣**    

  9

# **张涛**    

​     11

# **李传明**  

  11