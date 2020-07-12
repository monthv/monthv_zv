# U袋商城数据库

## 帮助中心

HelpCentre

| 字段    | 类型            | 约束 | 可空 | 备注       |
| ------- | --------------- | ---- | ---- | ---------- |
| HelpeId | int             | key  |      | id         |
| Doubt   | nvarchar（150） |      |      | 疑惑问题   |
| Result  | nvarchar（500） |      |      | 答案、结果 |

企业简介、新手上路、诚信合约、U袋学堂说明



## 用户角色

RoleInfo

| 字段     | 类型        | 约束 | 可空 | 备注     |
| -------- | ----------- | ---- | ---- | -------- |
| RoleId   | int         | key  |      | 角色id   |
| RoleName | varchar(20) |      |      | 角色名称 |



## 用户表

UserInfo

| 字段           | 类型         | 约束 | 可空 | 备注                       |
| -------------- | ------------ | ---- | ---- | -------------------------- |
| UserId         | int          | key  |      | 用户id                     |
| UserName       | nvarchar(20) |      |      | 用户名                     |
| Password       | varchar(50)  |      |      | md5密码                    |
| CreateTime     | datetime     |      |      | 注册时间                   |
| LastModifyTime | datetime     |      | null | 最后修改时间               |
| CheckedDay     | int          |      |      | 签到天数                   |
| Intrgral       | int          |      |      | 积分                       |
| Balance        | decimal      |      |      | 账户余额                   |
| PayPassword    | varchar(50)  |      |      | 支付密码                   |
| LoginFlag      | bit          |      |      | 账号状态 （非0账号表异常） |
|                |              |      |      |                            |



## 用户详情表

UserDetail

| 字段     | 类型        | 约束        | 可空 | 备注                  |
| -------- | ----------- | ----------- | ---- | --------------------- |
| UserId   | int         | foregin key |      | 用户表外键            |
| Gender   | bit         |             | null | 用户性别 (0:男 1：女) |
| Birthday | datetime    |             | null | 生日                  |
| Avatar   | varchar(50) |             | null | 头像                  |
| Phone    | varchar(20) |             | null | 电话                  |
| Email    | varchar(20) |             | null | 邮箱                  |



## 用户角色映射表

UserRoleMapping

| 字段   | 类型 | 约束                  | 可空 | 备注       |
| ------ | ---- | --------------------- | ---- | ---------- |
| UserId | int  | foregin key     `key` |      | 用户表外键 |
| RoleId | int  | foregin key   `key`   |      | 角色表外键 |



## 区域表

regions

| 字段     | 类型         | 约束 | 可空 | 备注         |
| -------- | ------------ | ---- | ---- | ------------ |
| id       | int          |      |      | 区域主键     |
| name     | varchar(40)  |      |      | 区域名称     |
| pid      | int          |      |      | 区域上级标识 |
| sname    | varchar(40)  |      |      | 地名简称     |
| level    | int          |      |      | 区域等级     |
| citycode | varchar(20)  |      |      | 区域编码     |
| yzcode   | varchar(20)  |      |      | 邮政编码     |
| mername  | varchar(100) |      |      | 组合名称     |
| Lng      | float        |      |      | 经度         |
| Lat      | float        |      |      | 纬度         |
| pinyin   | varchar(100) |      |      | 拼音         |



## 收货地址

ReceivingAddress

| 字段              | 类型         | 约束         | 可空 | 备注               |
| ----------------- | ------------ | ------------ | ---- | ------------------ |
| AddressId         | int          | key          |      | 地址id             |
| ReceivingName     | nvarchar(20) |              |      | 收货人姓名         |
| ProvinceId        | int          | foreginkey   |      | 省级id             |
| CityId            | int          | foreginkey   |      | 市级id             |
| DistrictCountyId  | int          | foreginkey   |      | 区县id             |
| `VillagesTownsId` | `int`        | `foreginkey` |      | `乡镇id（无此列）` |
| DetailedAddress   | nvarchar(50) |              |      | 详细地址           |
| Phone             | varchar(20)  |              |      | 手机               |
| IsDefault         | bit          |              |      | 是否为默认地址     |



## 店铺表

StoreInfo

| 字段           | 类型          | 约束 | 可空 | 备注                                                         |
| -------------- | ------------- | ---- | ---- | ------------------------------------------------------------ |
| StoreId        | int           | key  |      | 店铺id                                                       |
| StoreName      | nvarchar(50)  |      |      | 店铺名称                                                     |
| Logo           | varchar(50)   |      | null | 店铺logo                                                     |
| CreateTime     | datetime      |      |      | 注册时间                                                     |
| LastModifyTime | datetime      |      | null | 最后一次修改时间                                             |
| Descripition   | nvarchar(200) |      | null | 店铺描述                                                     |
| StoreState     | int           |      |      | 店铺状态（0：待审核，1：审核中，2：审核通过，3：审核不通过） |



## 店铺详情表

StoreDetail

| 字段            | 类型          | 约束        | 可空 | 备注                |
| --------------- | ------------- | ----------- | ---- | ------------------- |
| StoreId         | int           | forigin key |      | 店铺表外键          |
| Regionid        | int           | foregin key |      | 区域id              |
| Detailedaddress | nvarchar(100) |             |      | 详细地址            |
| Corporation     | nvarchar(20)  |             |      | 法人                |
| Idcard          | char(20)      |             |      | 法人身份证          |
| Phone           | varchar(20)   |             |      | 手机                |
| CustomServiceQQ | varchar(50)   |             |      | 客服qq，多个qq&隔开 |



## 优惠券表

Coupon

| 字段             | 类型     | 约束 | 可空 | 备注                                  |
| ---------------- | -------- | ---- | ---- | ------------------------------------- |
| CouponId         | int      | key  |      | 优惠券id                              |
| SubtractMoney    | decimal  |      |      | 优惠金额                              |
| PassMoney        | decimal  |      |      | 满多少可用                            |
| UseStartTime     | datetime |      |      | 开始使用时间                          |
| UseEndTime       | datetime |      | null | 结束使用时间                          |
| ProvideCount     | int      |      |      | 优惠券的发放数量                      |
| GetAuthorization | int      |      |      | 领取权限（0：任何人 1：粉丝 2：会员） |
| Stock            | int      |      |      | 库存数量                              |
|                  |          |      |      |                                       |



## 店铺优惠券映射表

StoreCouponMapping

| 字段     | 类型 | 约束            | 可空 | 备注       |
| -------- | ---- | --------------- | ---- | ---------- |
| StoreId  | int  | foregin key key |      | 店铺表外键 |
| CouponId | int  | foregin key key |      | 优惠券id   |



## 用户优惠券表

UserCoupon

| 字段        | 类型 | 约束        | 可空 | 备注       |
| ----------- | ---- | ----------- | ---- | ---------- |
| UserId      | int  | foregin key |      | 用户表id   |
| CouponId    | int  | foregin key |      | 优惠券id   |
| CouponCount | int  |             |      | 优惠券数量 |
| IsValid     | bit  |             |      | 是否有效   |



## 积分日志表

IntrgralLog

| 字段        | 类型         | 约束        | 可空 | 备注                        |
| ----------- | ------------ | ----------- | ---- | --------------------------- |
| UserId      | int          | foregin key |      | 用户表外键                  |
| LogType     | bit          |             |      | 日志类型（0：支出 1：收入） |
| Describe    | nvarchar(50) |             | null | 描述（为什么收入或支付）    |
| TradeNumber | int          |             |      | 支出或收入积分数            |



## 商品类型表

ProductCategory 

| 字段          | 类型         | 是否可null | 约束 | 备注                         |
| ------------- | ------------ | ---------- | ---- | ---------------------------- |
| CategoryId    | int          |            | key  | 商品分类id                   |
| CategoryName  | nvarchar(10) |            |      | 商品分类名称                 |
| ParentId      | int          |            |      | 父级id                       |
| CategoryLevel | int          |            |      | 分类级别自动维护  SaveChange |



## 商品表

Product

| 字段            | 类型          | 是否可null | 约束    | 备注                                |
| --------------- | ------------- | ---------- | ------- | ----------------------------------- |
| ProductId       | int           |            | key     | 商品id                              |
| ProductName     | nvarchar(100) |            |         | 商品名称                            |
| StoreId         | int           |            | forigin | 所属店铺id                          |
| CategoryId      | int           |            | forigin | 商品分类id                          |
| IsMarketable    | bit           |            |         | 是否上架                            |
| OldPrice        | decimel       |            |         | 商品原价                            |
| NewPrice        | decimel       |            |         | 商品售价                            |
| CreateTime      | datetime      |            |         | 创建时间                            |
| LastMidifyTime  | datetime      |            |         | 最后一次修改时间                    |
| MainImage       | varchar(80)   | null       |         | 商品主图                            |
| AssistImage     | varchar(300)  | null       |         | 辅助图片（多个图片路径之间用&隔开） |
| SellCount       | int           |            |         | 累计销量                            |
| LargessIntrgral | int           |            |         | 购买本商品赠送积分数                |
| Pigment         | nvarchar(50)  |            |         | 颜色（多种颜色用&隔开）             |
| Size            | nvarchar(50)  |            |         | 尺码（多种尺码用&隔开）             |
| Stock           | int           |            |         | 库存数量                            |
| Scale           | float         |            |         | 重量                                |
| TransportMoney  | decimal       |            |         | 运费                                |



## 商品收藏

ProductCollect

| 字段       | 类型     | 约束        | 可空 | 备注       |
| ---------- | -------- | ----------- | ---- | ---------- |
| UserId     | int      | foregin key |      | 用户表外键 |
| ProductId  | int      | foregin key |      | 商品表外键 |
| CreateTime | datetime |             |      | 添加时间   |



## 商品评论表

ProductComment

| 字段           | 类型            | 约束        | 可空 | 备注       |
| -------------- | --------------- | ----------- | ---- | ---------- |
| UserId         | int             | foregin key |      | 用户表主键 |
| Pigment        | nvarchar(50)    |             | null | 已购的颜色 |
| Size           | varchar(50)     |             | null | 已购的尺码 |
| ProductId      | int             | foreginkey  |      | 商品表外键 |
| CommentContent | nvarchar（500） |             | null | 评论内容   |
| CommentImage   | varchar(500)    |             | null | 评论图片   |
| CommentTime    | datetime        |             |      | 评论时间   |



## 运输公司表

TransportFirm

| 字段           | 类型         | 约束 | 可空 | 备注                                |
| -------------- | ------------ | ---- | ---- | ----------------------------------- |
| FirmId         | int          | key  |      | 公司id                              |
| FirmName       | nvarchar(50) |      |      | 公司名称                            |
| ChargingType   | bit          |      |      | 计费类型（0：按件计费 1：按重计费） |
| TransportMoney | decimal      |      |      | 计费（每件或每1kg多少钱）           |



## 店铺运输公司映射表

StoreTransportMapping

| 字段    | 类型 | 约束        | 可空 | 备注         |
| ------- | ---- | ----------- | ---- | ------------ |
| StoreId | int  | foregin key |      | 店铺外键     |
| FirmId  | int  | foregin key |      | 运输公司外键 |
|         |      |             |      |              |



## 订单表

OrderInfo

| 字段              | 类型          | 约束        | 可空       | 备注         |
| ----------------- | ------------- | ----------- | ---------- | ------------ |
| OrderId           | int           | key         |            | 订单id       |
| UserId            | int           | foergin key |            | 用户id       |
| StoreId           | int           | foregin key |            | 店铺id       |
| StoreName         | nvarchar(50)  |             |            | 店铺名称     |
| ProductId         | int           | foregin key |            | 商品id       |
| ProductName       | nvarchar(100) |             |            | 商品名称     |
| Pigment           | nvarchar(50)  |             |            | 颜色         |
| Size              | varchar(50)   |             |            | 尺码         |
| ProductCount      | int           |             |            | 商品数量     |
| Price             | decimal       |             |            | 商品单价     |
| RealPayMoney      | decimal       |             | null       | 实付款       |
| FirmId            | int           | foregin key | null       | 运输公司外键 |
| TransportFirmName | nvarchar(50)  |             | null       | 运输公司名称 |
| TransportMoney    | decimal       |             | default(0) | 运输费用     |
| CreateTime        | datetime      |             |            | 创建时间     |
| LastModifyTime    | datetime      |             | null       | 最后修改时间 |
| PayTime           | datetime      |             | null       | 支付时间     |
| TurnoverTime      | datetime      |             | null       | 成交时间     |
| AddressId         | int           | foregin key |            | 收货地址外键 |
| Buyerremark       | nvarcahr(100) |             |            | 卖家备注     |
|                   |               |             |            |              |



## 订单退款表

OrderRefunds

| 字段           | 类型          | 约束        | 可空 | 备注                          |
| -------------- | ------------- | ----------- | ---- | ----------------------------- |
| OrderId        | int           | foregin key |      | 订单id                        |
| OrderState     | bit           |             |      | 订单状态（0：审核中 1：成功） |
| Refundcause    | nvarchar(100) |             |      | 退款原因                      |
| CreateTime     | datetime      |             |      | 申请时间                      |
| LastModifyTime | datetime      |             | null | 最后修改时间                  |
| RefundsMoney   | decimal       |             | null | 退款金额                      |



## U袋学堂(视频)

CourseVideo

| 字段           | 类型         | 约束 | 可空 | 备注            |
| -------------- | ------------ | ---- | ---- | --------------- |
| CourseId       | int          | key  |      | 教程id          |
| CourseName     | nvarchar(50) |      |      | 教程名称        |
| Price          | decimal      |      |      | 价格(0表示免费) |
| VideoImage     | varchar(50)  |      |      | 视频首页图片    |
| VideoPath      | varchar(50)  |      |      | 视频相对地址    |
| CreateTime     | datetime     |      |      | 添加时间        |
| LastModifyTime | datetime     |      | null | 最后修改时间    |
|                |              |      |      |                 |
|                |              |      |      |                 |



## 购物车

ShoppingCart

| 字段         | 类型 | 约束        | 可空 | 备注       |
| ------------ | ---- | ----------- | ---- | ---------- |
| UserId       | int  | foregin key |      | 用户表外键 |
| ProductId    | int  | foregin key |      | 商品id     |
| ProductCount | int  |             |      | 商品数量   |
| IsDelete     | bit  |             |      | 是否删除   |



## 平台公告类型

NewsCategory 

| 字段         | 类型         | 约束 | 可空 | 备注     |
| ------------ | ------------ | ---- | ---- | -------- |
| CategoryId   | int          | key  |      | 分类id   |
| CategoryName | nvarchar(50) |      |      | 分类名称 |



## 平台公告

NewsInfo

| 字段           | 类型           | 约束        | 可空 | 备注         |
| -------------- | -------------- | ----------- | ---- | ------------ |
| NewsId         | int            | key         |      | 新闻id       |
| NewsTitle      | nvarchar(50)   |             |      | 新闻标题     |
| CategoryId     | int            | key         |      | 分类id       |
| CreateTime     | datetime       |             |      | 添加时间     |
| LastModifyTime | datetime       |             | null | 最后修改时间 |
| NewsContent    | nvarchar(1000) |             |      | 新闻内容     |
| IsDelete       | bit            |             |      | 是否删除     |
| ProductId      | int            | foregin key | null | 连接商品id   |
|                |                |             |      |              |



## 页面浏览量

PageViewCensus

| 字段        | 类型     | 约束 | 可空 | 备注       |
| ----------- | -------- | ---- | ---- | ---------- |
| CensusId    | int      | key  |      | id         |
| CensusCount | int      |      |      | 页面浏览量 |
| CensusTime  | datetime |      |      | 统计的时间 |
|             |          |      |      |            |



## 客户统计

CustomCensus

| 字段          | 类型     | 约束 | 可空 | 备注       |
| ------------- | -------- | ---- | ---- | ---------- |
| CensusId      | int      | key  |      | id         |
| RegisterCount | int      |      |      | 注册数量   |
| CensusTime    | datetime |      |      | 统计的时间 |
|               |          |      |      |            |



## 订单统计

OrderCensus

| 字段       | 类型     | 约束        | 可空 | 备注       |
| ---------- | -------- | ----------- | ---- | ---------- |
| CensusId   | int      | key         |      | id         |
| StoreId    | int      | foregin key |      | 店铺id     |
| UserId     | int      | foregin key |      | 用户id     |
| TradeMoney | decimal  |             |      | 交易金额   |
| CensusTime | datetime |             |      | 统计的时间 |



## 浏览历史表

BrowseHistories

| 字段          | 类型     | 约束        | 可空 | 备注             |
| ------------- | -------- | ----------- | ---- | ---------------- |
| UserId        | int      | foreginkey  |      | 用户表外键       |
| ProductId     | int      | foregin key |      | 商品表外键       |
| VisitCount    | int      |             |      | 访问次数         |
| LastVisitTime | datetime |             |      | 最后一次访问时间 |

