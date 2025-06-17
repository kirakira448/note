# 1. 架构

## 1.1. 商城界面

### 前端
vue3 + element-plus
### 后端
spring + postgresql

## 1.2. 后台管理

### 前端
vue3 + element-plus
### 后端
spring + postgresql

# 2. 功能

## 2.1. 首页

- 提供导航菜单或链接，让用户浏览不同的产品类别。

## 2.2. 产品列表页

- 产品缩略图，名称，价格
- 产品搜索，筛选

## 2.3. 产品详情页

- 单个产品详细信息展示
- sku选择
- 添加到购物车按钮

## 2.4. 购物车

- 展示已添加的产品列表
- 修改数量，删除产品
- 结算按钮

## 2.5. 订单详情

- 用户查看自己的订单记录

## 2.6. 用户主页

- 查看个人信息，查看订单信息
- 修改个人信息，更改密码

# 3. 数据结构

## 3.1. 产品表（product）：

- product_id	产品id
- name		产品名
- description	产品描述
- category_id	分类id
- image_url		图像url
- tags			产品tag(json)
- create_name	创建人
- create_time	创建时间
- is_deleted	是否删除

## 3.2. 产品规格表(product_spec)

- id			规格id
- product_id	产品id
- sku			库存单元唯一编码
- code                    型号
- spec          	规格信息(json)
- stock		库存数量
- create_name	创建人
- create_time	创建时间
- update_name
- update_time
- is_deleted	是否删除

### 3.2.1 价格单(price)
- id 
- product_spec_id
- price		价格
- inquiry_info      询价信息(json)
- inquiry_expiration_time 询价有效期
- promotion                      优惠
- promotion_start_time     优惠开始时间
- promotion_end_time      优惠结束时间
## 3.3. 类别表（category）：

- category_id	分类id
- name		分类名
- parent_id		父级id
- create_name	创建人
- create_time	创建时间
- is_deleted	是否删除

## 3.4. 购物车表（cart）：

- cart_id		购物车id
- user_id		用户id
- product_variants_id	产品id
- quantity		数量
- create_name	创建人
- create_time	创建时间
- is_deleted	是否删除
## 3.5. 订单表（order）：

- id		订单id
- user_id		用户id
- total_amount	总计
- status		订单状态
- details              订单详情(json)
- payment_method   支付方式
- payment_status      支付状态
- paid_amount           已支付货款
- order_date	订单日期
- delivery_option    运输方式
- delivery_status     运输状态
- address 		联系方式(json)
- staff                  负责人
- remark              备注
- log                    变更记录(json)
- create_name	创建人
- create_time	创建时间
- update_name
- update_time
- is_deleted	是否删除
### 3.5.1 订单详情（json）：

- order_detail_id	订单详情id
- order_id		订单id
- product_variants_id		规格id
- quantity		数量
- unit_price		单价
- create_name	创建人
- create_time	创建时间
- is_deleted	是否删除

## 3.6. 批次表
- id
- order_id
- detail      (product_variants_id, quantity)
- status          状态
- create_name	创建人
- create_time	创建时间
- update_name
- update_time
- is_deleted	是否删除
## 3.7. 用户表（user）：

- user_id		用户id
- username		用户名
- password		密码
- role                  角色
- email		邮箱
- address		地址
- phone		电话
- create_name	创建人
- create_time	创建时间
- is_deleted	是否删除

## (deleted)3.8. 支付方式表(user_payment_method)

- id
- user_id
- method                       支付方式
- info                              信息（json）

## (deleted)3.9. 支付表（payment）

- id
- order_id                
- status                     状态
- method                  方式
- amount                  总计
- remark
- log
- pay_time                 支付时间
- create_name	创建人
- create_time	创建时间
- update_name
- update_time
- is_deleted	是否删除


# 4. 产品分类

## 一级分类
**按照领域分类：**
Light Vehicle
Commercial Vehicle
Off-Highway
...

## 二级分类
**按照应用场景分类：**
Passenger Car
Light Truck
...

Linehaul
Heavy-Haul
...

## 三级分类
**按照部件位置/功能分类：**
Drive
Systems
Electrodynamic

## 筛选
**根据产品tag筛选产品列表**




# 5. 询价流程
## 业务逻辑
当创建订单的产品列表中有需要询价的产品时，拒绝创建订单
只允许创建确定价格的产品

询价的状态在 **商品规格表(product_variants)** 的inquiry_info字段

询价得到结果后，更新price字段，在商城中正常显示价格与价格有效期，通知客户下单

