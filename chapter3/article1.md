# HTML5游戏接入文档

## 文档修订记录

| 编号 | 日期 | 说明 |
| --- | --- | --- |
| 01 | 2019.01.15 | 初始版本 |
| 02 |  |  |

## 接入流程概述

1. CP需要在《西瓜平台》注册成为企业开发者，并创建类型为H5页游的游戏。
2. 录入相关信息后，会提供CP游戏接口实现所需的XgAppId和XgAppKey。
3. 平台提供给CP使用的XGJSSDK地址为：[https://h5ex.xgsdk.com/ex/sdk/xgsdk.js](https://h5ex.xgsdk.com/ex/sdk/xgsdk.js)
   CP需在游戏中集成该SDK，并通过此SDK调用平台提供的接口。
4. 平台测试环境

   > CP在完成上述过程后可以访问此链接地址进行集成测试：XXXXXXXXXXXXXXXXX  
   > 其中gameId为上述过程中平台提供给CP的gameId。

   ![](/img/structure.png)

## 接口

### 1.用户登录

* **接口:**
  **window.XGSDK.login\(authInfo\)**
* **接口说明**
  > 玩家角色进入游戏时调用
* **代码**

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

  ### 2.退出游戏

* **接口:**  
  **window.XGSDK.exit\(\)**

* **接口说明**

  > 玩家角色退出游戏时调用

* **代码**

  ```js
  function(){
    console.log('exit game...');
    window.XGSDK.exit();
    }
  ```

  ### 3.支付充值

* **接口:**  
  **window.XGSDK.pay\(orderInfo,callback\)**

* **接口说明**

  > 玩家角色充值时调用

* **代码**

  ```js
  var orderInfo = {
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
    currencyName:'CNY',
    uid:'123456'
    };
    window.XGSDK && window.XGSDK.pay(orderInfo, function(msg){
            console.log(msg);
    });
  ```

  ### 4.数据上报

* **接口:**  
  **window.XGSDK.dataReport\(data\)**

* **接口说明**

  > 玩家角色上报数据时调用

* **代码**

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

  ### 5.分享

* **接口:**  
  **window.XGSDK.share\(shareInfo, callback\)**

* **接口说明**

  > 玩家角色分享时调用

* **代码**
  ```js
  function(){
    window.XGSDK.share('share game...');
    }
  ```



