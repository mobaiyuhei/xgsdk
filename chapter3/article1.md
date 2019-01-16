

# HTML5游戏接入文档

## 文档修订记录

编号 | 日期 |说明
---|---|---
01 | 2019.01.15 | 初始版本
02 |  | 

## 接入流程概述
1. CP需要在对接的QQ讨论组中将游戏信息提供给我方运营或商务接口人，获取接入SDK所需的参数：

- 开发者需提供的信息：

参数名称 |描述
---|---|---
gameName | 游戏名称
icon | 游戏图标，线下提供图片
orientation | 游戏横竖屏， 0 ：竖屏；1 ：横屏
gameAddr | 游戏原始地址，如：http://www.xxx.game.com
payCallback_Url | 支付回调地址，用于接收支付结果通知

- 我方分配的参数：

参数名称 |参数类型|描述
---|---|---
xgAppId | string| 游戏在西瓜SDK的唯一标识
key | string| 游戏服务端与SDK服务端通信校验使用（由于涉及到加密通信，开发者必须严格对 key 进行保密仅服务端使用，不能写到客户端代码中）

2. 平台联运xgsdk
> 平台提供给CP使用的xgsdk地址为：https://h5ex.xgsdk.com/ex/sdk/xgsdk.js<br>
> CP需在游戏中集成该SDK，并通过此SDK调用平台提供的接口。

3. 平台测试环境
> CP在完成上述过程后可以访问此链接地址进行集成测试：XXXXXXXXXXXXXXXXX
其中gameId为上述过程中平台提供给CP的gameId。

4. 平台游戏集成架构图
![](/img/structure.png)

## 接口
### 0.引用SDK【必接】
在<head>中引用SDK脚本如：
```html
<script type="text/javascript" src="https://h5ex.xgsdk.com/ex/sdk/xgsdk.js"></script>
```

### 1.用户登录【选接】
- **接口:**
  **window.XGSDK.login(authInfo)**
- **接口说明**
> 初始化SDK，设置全局参数.玩家角色进入游戏时调用
- **代码**
```js
authInfo = {
    xgAppId:'91000184',
    planId:'2079',
    channelId:'jinshan',
    ts: 1547541807,
    authToken:'eda3db00c5a6624a',
    uid: '123456',
    extData: '{"version":"4.0.6"}'
    };
window.XGSDK.login(authInfo);
```
### 2.退出游戏【必接】
- **接口:**
  **window.XGSDK.exit()**
- **接口说明**
> 玩家角色退出游戏时调用
- **代码**
```js
function(){
    console.log('exit game...');
    window.XGSDK.exit();
    }
```
### 3.支付充值【必接】
- **接口:**
  **window.XGSDK.pay(orderInfo,callback)**
- **接口说明**
> 游戏页面打开收银台进行支付充值时调用
- **代码**
```js
var orderInfo = {
    uid:'123456',
    productId: '80',
    productName: '测试币',
    productQuantity: 1,
    productUnitPrice: 100,
    totalAmount: 100,
    paidAmount: 100,
    gameTradeNo: '123456789987456321',
    productUnitPrice: 100,
    roleId: '10008916',
    roleName: '风一样的女子',
    roleType: '法师', 
    roleLevel: '10', 
    roleVipLevel: '10',  
    zoneId: '512',  
    zoneName: '测试',  
    serverId: '1200',
    serverName: '测试服',  
    currencyName:'CNY'
    };
    window.XGSDK.pay(orderInfo, function(msg){
            console.log(msg);
    });
```
- **关于 PayInfo 的成员说明**

请严格按照西瓜规定的字段长度进行设置，否则可能发生游戏服务器端长度不够问题。


| 参数  | 参数类型  | 最大长度  | 说明  | 必须  |
| :------------ | :------------: | :------------: | :------------ | :------------: |
| uid | string | 128 | 用户ID,游戏必须使用登录时西瓜服务器返回的uid | Y |
| productId | string | 64 | 商品ID | Y |
| productName | string | 64 | 商品名称 | Y |
| productDesc | string | 128 | 商品描述 | Y |
| productUnit | string | 64 | 商品单位，例如元宝 | Y |
| productUnitPrice | int | 10 | 商品单价,单位分（无需传，以后版本会去掉） | N |
| productQuantity | int | 10 | 产品数量，例如购买60元宝则传60 | Y |
| totalAmount | int | 10 | 商品总金额,单位分  | Y |
| payAmount | int | 10 |  实际支付总额,单位分< | Y |
| currencyName | string | 64 | 海外渠道必传：实际支付的国际标准货币代码，比如CNY(人民币)/USD(美元) | Y |
| roleId | string | 32 | 角色ID | Y |
| roleName | string | 64 | 角色名称 | Y |
| roleLevel | int | 32 | 角色等级 | Y |
| roleVipLevel | int | 32 | 角色vip等级  | Y |
| serverId | string | 32 | 服ID：必须为纯数字，且不能超过2147483647（应用宝渠道要求） | Y |
| zoneId | string | 32 | 区ID | Y |
| partyName | string | 32 | 帮会名称  | N |
| virtualCurrencyBalance | string |  | 虚拟货币余额，需要此字段的渠道：快发、小米、VIVO  | Y |
| customInfo | string | 2000 | 扩展字段，订单支付成功后，透传给游戏 | N |
| gameTradeNo | string | 64 | 游戏订单ID，支付成功后，透传给游戏 | N |
| gameCallbackUrl | string ||128 支付回调地址，如果为空，则后台配置的回调地址  | N |
| additionalParams | string |  | 扩展参数 |  N |

### 4.数据上报【必接】
- **接口:**
  **window.XGSDK.dataReport(data)**
- **接口说明**
> 玩家角色上报数据时调用
- **代码**
```js
var roleInfo={
        msgType: 'role.login',
        accountId: 'uc_29c4bb6d76924a86c020397c94d2b138',
        roleId: '10008916',  
        roleName: '风一样的女子',   
        roleType: '法师',            //角色类型,如法师，道士，战士
        roleLevel: '10',            //角色等级
        roleVipLevel: '10',         //角色vip等级
        zone: '512',                //游戏区ID
        zoneName: '测试',            //游戏区名称
        server: '1200',            //游戏服ID,示例:s1,s2
        serverName: '测试服',        //游戏服名称,示例:风云争霸
        partyId: '',            //公会ID
        gender: 'f',            //角色性别 m:男 f:女
        battleScore: '100'   
        };
window.XGSDK.dataReport(roleInfo);
```
-  **关于 RoleInfo 的成员说明：**

请严格按照西瓜规定的字段长度进行设置，否则可能发生游戏服务器端长度不够问题。

|  参数 |  参数类型 | 最大长度| 说明  |  必须 |
| :--- | :---: | :---: | --- | :---: |
| uid | string | 128 | 用户ID,游戏必须使用登录时西瓜服务器返回的uid |Y |
| serverId | string |  32 | 服ID：必须为纯数字，且不能超过2147483647（应用宝渠道要求） |Y |
| serverName | string | 64  | 游戏必须传入真实的游戏服名称,建议中文 |Y |
| zoneId | string  | 32  | 游戏区ID |Y |
| zoneName | string | 64  |游戏大区名称：要与界面显示名称一致，如：界面显示（一区 桃园结义），zoneName也必须传（一区 桃园结义），UC渠道要求必传真实值，否则无法通过审核   |Y |
| roleId | string |  32 |  角色ID |Y |
| roleName | string | 64  | 角色名  |Y |
| roleType | string |  20 | 角色类型，如法师，道士，战士  |N |
| roleCreateTime | string  | 10  | 角色创建时间（Unix时间戳，单位秒），如：1461722392，UC渠道要求必传真实值，否则无法通过审核  |Y |
| roleLevel | int | 32  | 角色等级,游戏必须传入真实的角色等级  |Y |
| roleVipLevel | int |  32 |  角色vip等级   |N |
| partyName | string | 32  |  公会名 |N |
| gender | string |
m:男;f:女 |  角色性别 |N |
| balance | string |  128 | 角色账户余额  |N |

### 5.分享【必接】
- **接口:**
  **window.XGSDK.share(shareInfo, callback)**
- **接口说明**
> 玩家角色分享时调用
- **代码**
```js
function(){
        window.XGSDK.share('share game...',function(msg){
                console.log(msg);
        });
    }
```
