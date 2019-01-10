# HTML5游戏使用西瓜SDK接入文档 {#html5游戏使用西瓜sdk接入文档}

## 0. 目录 {#0-目录}

1. 目录

2. 文档概述

3. 用户与角色接口

   1. 2.1 西瓜SDK初始化回调
      1. 2.1.1 初始化成功
      2. 2.1.2 初始化失败
   2. 2.2 登录接口（必接）
   3. 2.3 登录回调
      1. 2.3.1 登录成功
      2. 2.3.2 登录失败
      3. 2.3.3 登录取消
   4. 2.4 登出接口
   5. 2.5 登出回调
   6. 2.6 退出接口（必接）
   7. 2.7 退出回调
      1. 2.7.1 已提供退出引导
      2. 2.7.2 未提供退出引导
   8. 2.8 释放资源接口

4. 充值接口

   1. 3.1 支付接口（必接）
   2. 3.2 支付回调
      1. 3.2.1 支付成功
      2. 3.2.2 支付失败
      3. 3.2.3 支付取消
      4. 3.2.4 支付其他状态
      5. 3.2.5 支付进度

5. 统计接口

   1. 4.1 创建角色（必接）
   2. 4.2 角色升级（必接）
   3. 4.3 进入游戏（必接）

6. 扩展接口

   1. 5.1 切换账号
   2. 5.2 自定义事件
   3. 5.3 任务开始
   4. 5.4 任务成功
   5. 5.5 任务失败
   6. 5.6 购买虚拟货币
   7. 5.7 赠送虚拟货币
   8. 5.8 消费虚拟货币

7. 运营活动接口

   1. 6.1 礼包码兑换，绑定手机号\(西瓜提供页面\)
   2. 6.2 礼包码兑换 （游戏提供界面）
   3. 6.3 绑定手机号（游戏提供界面）
   4. 6.4 问卷调查（游戏提供界面）
      1. 6.4.1 初始化问卷
      2. 6.4.2 刷新问卷
      3. 6.4.3 打开问卷
   5. 6.5 更新服务回调接口

8. 渠道接入要点须知

## 1. 文档概述 {#1-文档概述}

此文档为h5小游戏使用西瓜原生SDK 登录支付引擎的接入文档。

本文介绍如何在h5的平台中，快速接入西瓜SDK，实现混合开发。

文档介绍各个接口的接入说明和样例代码。

逐步细述了整个接入过程,同时罗列出了5种类型的接口：分别为：用户与角色接口、充值接口、统计接口、扩展接口、运营活动接口，便于游戏方的接入人员可以按照需求更加快速便捷的进行接入。

**其他**:创建产品和申请渠道参数 请前往西瓜SDK官网查看.[传送门](https://www.xgsdk.com/doc/section1/index.html)

## 2. 用户与角色接口 {#2-用户与角色接口}

### 2.1 西瓜SDK初始化回调 {#21-西瓜sdk初始化回调}

#### 2.1.1 初始化成功 {#211-初始化成功}

* **接口function onXGInitSuccess\(data\)**

* **接口说明**

> 西瓜 SDK 初始化成功时,主动调用

* **代码**

```js
function
onXGInitSuccess(data) 
{
	document.getElementById("log_msg").innerHTML = ("onXGInitSuccess..."+ data);
}
```

* **输出数据格式**

```js
{
"code": 10001,  //返回码
"msg": "初始化成功",    //返回信息
"channelCode": "10010"      // 渠道编号
}
```

#### 2.1.2 初始化失败 {#212-初始化失败}

* **接口function onXGInitFail\(data\)**

* **接口说明**

> 西瓜 SDK 初始化失败时,主动调用

* **代码**

```js
function onXGInitFail(data) {
    document.getElementById("log_msg").innerHTML = ("onXGInitFail... " + data);
}
```

* **输出数据格式**

```js
{
"code": 10001,  //返回码
"msg": "初始化失败",    //返回信息
"channelCode": "10010"      // 渠道编号
}
```

### 2.2 登录接口（必接） {#22-登录接口必接}

* **接口window.XGAndroid.callXGLogin\(\)**

* **接口说明**

> 用户登录接口

* **参数说明**

> 无

* **代码**

```js
 <button id="btn_login" onclick="window.XGAndroid.callXGLogin()">调用 西瓜SDK 【login】</button>
```

### 2.3 登录回调 {#23-登录回调}

#### 2.3.1 登录成功 {#231-登录成功}

* **接口function onXGLoginSuccess\(data\)**

* **接口说明**

> 登录成功时调用

* **代码**

```js
function onXGLoginSuccess(data) {
    document.getElementById("log_msg").innerHTML = ("onXGLoginSuccess... " + data);
}
```

* **输出数据格式**

```js
{
"code": 200,  //返回码
"authInfo": "eyJhdXRoVG9r...jZTA5",    //验证返回值信息
}
```

* **注意:**

> 可以在此接口中调用 callXGEnter\(roleInfo\) 接口。

#### 2.3.2 登录失败 {#232-登录失败}

**接口function onXGLoginFail\(data\)**

* **接口说明**

> 登录失败时调用

* **代码**

```js
 function onXGLoginFail(data) {
    document.getElementById("log_msg").innerHTML = ("onXGLoginFail... " + data);
}
```

* **输出数据格式**

```js
{
"code": 10001,  //返回码
"msg": "用户登录失败",    //返回信息
"channelCode": "10010"      // 渠道编号
}
```

#### 2.3.3 登录取消 {#233-登录取消}

* **接口function onXGLoginCancel\(data\)**

* **接口说明**

> 登录取消时调用

* **代码**

```js
 function onXGLoginCancel(data) {
    document.getElementById("log_msg").innerHTML = ("onXGLoginCancel... " + data);
}
```

* **输出数据格式**

```js
{
"code": 10001,  //返回码
"msg": "用户登录取消",    //返回信息
}
```

### 2.4 登出接口 {#24-登出接口}

* **接口window.XGAndroid.callXGLogout\(\)**

* **接口说明**

> 用户登出接口

* **参数说明**

> 无

* **代码**

```js
<button id="btn_logout" onclick="window.XGAndroid.callXGLogout()">调用 西瓜SDK 【logout】</button>
```

### 2.5 登出回调 {#25-登出回调}

**接口function onXGLogoutFinish\(data\)**

* **接口说明**

> 用户调用callXGLogout\(\)后回调

* **代码**

```js
function onXGLogoutFinish(data) {
    document.getElementById("log_msg").innerHTML = ("onXGLogoutFinish... " + data);
}
```

* **输出数据格式**

```js
{
"code": 200,  //返回码
"msg": "用户退出登录",    //返回信息
}
```

### 2.6 退出接口（必接） {#26-退出接口必接}

* **接口window.XGAndroid.callXGExit\(\)**

* **接口说明**

> 用户退出接口

* **参数说明**

> 无

* 代码

```js
<button id="btn_exit" onclick="window.XGAndroid.callXGExit()">调用 西瓜SDK 【exit】</button>
```

### 2.7 退出回调 {#27-退出回调}

#### 2.7.1 已提供退出引导 {#271-已提供退出引导}

* **接口function onXGdoExit\(\)**

* **接口说明**

> 已提供退出引导,callXGExit\(\)回调,游戏需要使用自己的退出引导，进行退出

* **代码**

```js
function onXGdoExit() {
    document.getElementById("log_msg").innerHTML = ("onXGdoExit... 已提供退出引导，游戏不需要使用自己的退出引导");
}
```

#### 2.7.2 未提供退出引导 {#272-未提供退出引导}

* **接口function onXGNoChannelExiter\(\)**

* **接口说明**

> 已提供退出引导,callXGExit\(\)回调,游戏不需要使用自己的退出引导

* **代码**

```js
function onXGNoChannelExiter(code, msg) {
    document.getElementById("log_msg").innerHTML = ("onXGNoChannelExiter... 未提供退出引导,游戏需要使用自己的退出引导，进行退出");
}
```

### 2.8 释放资源接口 {#28-释放资源接口}

* **接口window.XGAndroid.callXGReleaseResource\(\)**

* **接口说明**

> 进入游戏接口，进入游戏时调用

* **参数说明**

> 无

* **代码**

```js
<button id="btn_release" onclick="window.XGAndroid.callXGReleaseResource()">调用 西瓜SDK 【release source】</button>
```

* **注意:**

> 游戏在调用退出接口时,已经调用了此接口,无需再次调用.若除了退出游戏还有其他地方使用,可调用此接口释放资源

## 3.充值接口 {#3充值接口}

### 3.1 支付接口（必接） {#31-支付接口必接}

* **接口window.XGAndroid.callXGPay\(payInfo\)**

* **接口说明**

> 充值接口

* **参数说明**

> **payInfo:**支付信息，包含产品ID、名称和数量等,传输时使用 json 格式

* **代码**

```js
html代码:
  <button id="btn_pay" onclick="pay()">调用 西瓜SDK 【pay】</button>
js代码:

function pay() {
    var info={};
    info.uid='uc_29c4bb6d76924a86c020397c94d2b138';
    info.productId='com.sho';
    info.productName='60这种';
    info.productDesc='6元购买60元宝';
    info.productUnit='这种';
    info.currencyName='CHN';
    info.roleId='10008916';
    info.roleName='123';
    info.roleLevel='1';
    info.roleVipLevel='0';
    info.gameCallbackUrl='';
    info.additionalParams='';
    info.productUnitPrice=1;
    info.productQuantity=60;
    info.totalAmount=60;
    info.payAmount=60;
    window.XGAndroid.callXGPay(JSON.stringify(info));
}
```

* **关于 PayInfo 的成员说明**

**所有必字段必须进行接入，否则会导致部分渠道无法支付！**请严格按照西瓜规定的字段长度进行设置，否则可能发生游戏服务器端长度不够问题。

| 参数 | 参数类型 | 最大长度 | 说明 | 必须 |
| :--- | :--- | :--- | :--- | :--- |
| uid | string | 128 | 用户ID,游戏必须使用登录时西瓜服务器返回的uid | Y |
| productId | string | 64 | 商品ID | Y |
| productName | string | 64 | 商品名称 | Y |
| productDesc | string | 128 | 商品描述 | Y |
| productUnit | string | 64 | 商品单位，例如元宝 | Y |
| productUnitPrice | int | 10 | 商品单价,单位分（无需传，以后版本会去掉） | N |
| productQuantity | int | 10 | 产品数量，例如购买60元宝则传60 | Y |
| totalAmount | int | 10 | 商品总金额,单位分 | Y |
| payAmount | int | 10 | 实际支付总额,单位分&lt; | Y |
| currencyName | string | 64 | 海外渠道必传：实际支付的国际标准货币代码，比如CNY\(人民币\)/USD\(美元\) | Y |
| roleId | string | 32 | 角色ID | Y |
| roleName | string | 64 | 角色名称 | Y |
| roleLevel | int | 32 | 角色等级 | Y |
| roleVipLevel | int | 32 | 角色vip等级 | Y |
| serverId | string | 32 | 服ID：必须为纯数字，且不能超过2147483647（应用宝渠道要求） | Y |
| zoneId | string | 32 | 区ID | Y |
| partyName | string | 32 | 帮会名称 | N |
| virtualCurrencyBalance | string |  | 虚拟货币余额，需要此字段的渠道：快发、小米、VIVO | Y |
| customInfo | string | 2000 | 扩展字段，订单支付成功后，透传给游戏 | N |
| gameTradeNo | string | 64 | 游戏订单ID，支付成功后，透传给游戏 | N |
| gameCallbackUrl | string |  | 128 支付回调地址，如果为空，则后台配置的回调地址 | N |
| additionalParams | string |  | 扩展参数 | N |

* **常用的国际货币**

| 国家 | 货币中文名 | 货币英文名 | 货币代码 |
| :--- | :--- | :--- | :--- |
| 中国 | 人民币元 | RenminbiYuan | CNY |
| 韩国 | 韩圆 | Korean Won | KRW |
| 日本 | 日元 | Japanese Yen | JPY |
| 美国 | 美元 | U.S.Dollar | USD |

* **关于 PayResult 的成员说明**

| 参数 | 说明 |
| :--- | :--- |
| code | 返回值码 |
| msg | 返回值信息 |
| gameTradeNo | 游戏订单ID，支付成功后，透传给游戏 |
| xgTradeNo | 西瓜平台游戏订单ID |
| channelCode | 渠道编号 |
| channelMsg | 渠道返回消息信息 |

### 3.2 支付回调 {#32-支付回调}

#### 3.2.1 支付成功 {#321-支付成功}

* **接口function onXGPaySuccess\(data\)**

* **接口说明**

> 支付成功时调用

* **参数说明**

> * **payInfo:**
>   支付信息对象，包含产品ID、名称和数量等 \(json字符串\)
> * **payResult:**
>   支付结果 \(json字符串\)

* **代码**

```js
 function onXGPaySuccess(data) {
    document.getElementById("log_msg").innerHTML = ("onXGPaySuccess... "+ data);
}
```

* **输出数据格式**

```js
{
    "payInfo": {   //详细参考【关于 PayInfo 的成员说明】
        "uid": "123",
        "productId": "123456",
        "productName": "金币",
        ....
    },
    "payResult": {
        "code": 200,
        "msg": "支付",
        "gameTradeNo": "12235445",
        "xgTradeNo": "122545",
        "channelCode": "10010",
        "channelMsg": "小米"
    }
}
```

#### 3.2.2 支付失败 {#322-支付失败}

* **接口function onXGPayFail\(data\)**

* **接口说明**

> 支付失败时调用

* **参数说明**

> * **payInfo:**
>   支付信息对象，包含产品ID、名称和数量等 \(json字符串\)
> * **payResult:**
>   支付结果 \(json字符串\)

* **代码**

```js
function onXGPayFail(data) {
    document.getElementById("log_msg").innerHTML = ("onXGPayFail... "+ data);
}
```

* **输出数据格式**

```js
{
    "payInfo": {  //详细参考【关于 PayInfo 的成员说明】
        "uid": "123",
        "productId": "123456",
        "productName": "金币",
        ....
    },
    "payResult": {
        "code": 200,
        "msg": "支付",
        "gameTradeNo": "12235445",
        "xgTradeNo": "122545",
        "channelCode": "10010",
        "channelMsg": "小米"
    }
}
```

#### 3.2.3 支付取消 {#323-支付取消}

* **接口function onXGPayCancel\(data\)**

* 接口说明

> 支付取消时调用

* 参数说明

> * **payInfo:**
>   支付信息对象，包含产品ID、名称和数量等 \(json字符串\)
> * **payResult:**
>   支付结果 \(json字符串\)

* **代码**

```js
function onXGPayCancel(data) {
    document.getElementById("log_msg").innerHTML = ("onXGPayCancel.. "+ data);
}
```

* **输出数据格式**

```js
{
    "payInfo": {   //详细参考【关于 PayInfo 的成员说明】
        "uid": "123",
        "productId": "123456",
        "productName": "金币",
        ....
    },
    "payResult": {
        "code": 200,
        "msg": "支付",
        "gameTradeNo": "12235445",
        "xgTradeNo": "122545",
        "channelCode": "10010",
        "channelMsg": "小米"
    }
}
```

#### 3.2.4 支付其他状态 {#324-支付其他状态}

**接口function onXGPayOthers\(data\)**

* **接口说明**

> 其他支付状态时调用

* **参数说明**

> * **payInfo:**
>   支付信息对象，包含产品ID、名称和数量等 \(json字符串\)
> * **payResult:**
>   支付结果 \(json字符串\)

* **代码**

```js
function onXGPayOthers(data) {
    document.getElementById("log_msg").innerHTML = ("onXGPayOthers... "+ data);
}
```

* **输出数据格式**

```js
{
    "payInfo": {   //详细参考【关于 PayInfo 的成员说明】
        "uid": "123",
        "productId": "123456",
        "productName": "金币",
        ....
    },
    "payResult": {
        "code": 200,
        "msg": "支付",
        "gameTradeNo": "12235445",
        "xgTradeNo": "122545",
        "channelCode": "10010",
        "channelMsg": "小米"
    }
}
```

#### 3.2.5 支付进度 {#325-支付进度}

* **接口function onXGPayProgress\(data\)**

* **接口说明**

> 支付进度更新时调用

* **参数说明**

> * **payInfo:**
>   支付信息对象，包含产品ID、名称和数量等 \(json字符串\)
> * **payResult:**
>   支付结果 \(json字符串\)

* **代码**

```js
function onXGPayProgress(data) {
    document.getElementById("log_msg").innerHTML = ( "onXGPayProgress... "+ data);
}
```

* **输出数据格式**

```js
{
    "payInfo": {   //详细参考【关于 PayInfo 的成员说明】
        "uid": "123",
        "productId": "123456",
        "productName": "金币",
        ....
    },
    "payResult": {
        "code": 200,
        "msg": "支付",
        "gameTradeNo": "12235445",
        "xgTradeNo": "122545",
        "channelCode": "10010",
        "channelMsg": "小米"
    }
}
```

## 4.统计接口 {#4统计接口}

### 4.1 创建角色（必接）

- **接口**
**window.XGAndroid.callXGCreateRole(roleInfo)**

- **接口说明**
> 使用 roleInfo 来创建角色
- **参数说明**
> **roleInfo:** 角色信息,无传输时使用 (json字符串)
   
- **代码**

```js
html代码:
  <button id="btn_create_role" onclick="createRole()">调用 西瓜SDK 【create role】</button>
js代码:

function createRole() {
    var info={};
    info.uid='uc_29c4bb6d76924a86c020397c94d2b138';
    info.serverId='1200';
    info.serverName='测试123';
    info.zoneId='123456';
    info.zoneName='测试124';
    info.roleId='10008916';
    info.setRoleCreateTime=Date.parse(new Date());
    info.roleName='123';
    info.roleLevel='1';
    console.log(info)
    window.XGAndroid.callXGCreateRole(JSON.stringify(info));
}
```

-  **关于 RoleInfo 的成员说明：**

**所有必字段必须进行接入，否则会导致统计不完全，部分渠道审核无法通过！**
请严格按照西瓜规定的字段长度进行设置，否则可能发生游戏服务器端长度不够问题。

|  参数 |  参数类型 | 最大长度| 说明  |  必须 |
| :------------ | :------------: | :------------: | :------------ | :------------: |
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
| gender | string |  枚举值：m,f;分别代表男女 |  角色性别 |N |
| balance | string |  128 | 角色账户余额  |N |

### 4.2 角色升级（必接）

- **接口**
**window.XGAndroid.callXGUpdateRole(roleInfo)**

- **接口说明**
> 角色等级接口，角色等级提升时调用
- **参数说明**
>  **roleInfo:** 角色信息,无传输时使用 (json字符串)
   
- **代码**

```js
html代码:
 <button id="btn_update_role" onclick="updateRole()">调用 西瓜SDK 【update role】</button>
js代码:

  function updateRole() {
      var info={};
      info.uid='uc_29c4bb6d76924a86c020397c94d2b138';
      info.serverId='1200';
      info.serverName='测试123';
      info.zoneId='123456';
      info.zoneName='测试124';
      info.roleId='10008916';
      info.setRoleCreateTime=Date.parse(new Date());
      info.roleName='123';
      info.roleLevel='12';
      window.XGAndroid.callXGUpdateRole(JSON.stringify(info));
}
```

### 4.3 进入游戏（必接）

- **接口**
**window.XGAndroid.callXGEnter(roleInfo)**

- **接口说明**
> 进入游戏接口，进入游戏时调用
- **参数说明**
>  **roleInfo:** 角色信息,无传输时使用  (json字符串)
   
- **代码**

```js
html代码:
 <button id="btn_enter_game" onclick="enterGame()">调用 西瓜SDK 【enter game】</button>

js代码:

  function enterGame() {
      var info={};
      info.uid='uc_29c4bb6d76924a86c020397c94d2b138';
      info.serverId='1200';
      info.serverName='测试123';
      info.zoneId='123456';
      info.zoneName='测试124';
      info.roleId='10008916';
      info.setRoleCreateTime=Date.parse(new Date());
      info.roleName='123';
      info.roleLevel='1';
      window.XGAndroid.callXGEnter(JSON.stringify(info));
  }
```
- **注意:**
>  建议在所有的User Role Server 信息都获取到以后再进行调用

---
**待定未接!!!!!!!**

## 5.扩展接口 
### 5.1 切换账号
- **接口**
**window.XGAndroid.callXGSwitchAccount()**

- **接口说明**
> 切换账号
- **参数说明**
>  无
   
- **代码**

```js
html代码:
 <button id="btn_switch_account" onclick="switchAccount()">调用 西瓜SDK 【switch account】</button>

js代码:

function switchAccount() {
     window.XGAndroid.callXGSwitchAccount();
}
```
### 5.2 自定义事件
- **接口**
**window.XGAndroid.callXGSwitchAccount(data)**

- **接口说明**
> 自定义事件，传入事件id以及事件内容
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
  <button id="btn_event" onclick="myEvent()">调用 西瓜SDK 【event】</button>

js代码:

function myEvent() {
     var roleInfo={};
     roleInfo.uid='uc_29c4bb6d76924a86c020397c94d2b138';
     roleInfo.serverId='1200';
     roleInfo.serverName='测试123';
     roleInfo.zoneId='123456';
     roleInfo.zoneName='测试124';
     roleInfo.roleId='10008916';
     roleInfo.setRoleCreateTime=Date.parse(new Date());
     roleInfo.roleName='123';
     roleInfo.roleLevel='1';
     console.log(roleInfo)
     var eventBody={};
     eventBody.name='点击事件';
     eventBody.id='123';
     var eventId='111';
     var eventDesc='测试点击事件';
     var eventVal=111;
     var data={};
     data.roleInfo=roleInfo;
     data.eventBody=eventBody;
     data.eventId=eventId;
     data.eventDesc=eventDesc;
     data.eventVal=eventVal;
     console.log(data)
     window.XGAndroid.callXGEvent(JSON.stringify(data));
}
```

- **输入数据格式**

```js
{
    "roleInfo": {   //角色信息,参数参考【关于 RoleInfo 的成员说明】
        "uid": "uc_29c4bb6d76924a86c020397c94d2b138",
        "roleId": "10008916",
        "roleType": "create",
        "roleLevel": "1",
        ...
    },
    "eventId": "111", //事件ID
    "eventDesc": "测试点击事件",   //事件描述
    "eventVal": 111,    //事件内容
    "eventBody": {    //key-value 事件体
        "name": "点击事件",
        "id": "123"，
        ...
    }
}

```
### 5.3 任务开始
- **接口**
**window.XGAndroid.callXGMissionBegin(data)**

- **接口说明**
> 任务开始接口
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
   <button id="btn_mission_begin" onclick="missionBegin()">调用 西瓜SDK 【MissionBegin】</button>

js代码:

function missionBegin() {
     var roleInfo={};
     roleInfo.uid='uc_29c4bb6d76924a86c020397c94d2b138';
     roleInfo.serverId='1200';
     roleInfo.serverName='测试123';
     roleInfo.zoneId='123456';
     roleInfo.zoneName='测试124';
     roleInfo.roleId='10008916';
     roleInfo.setRoleCreateTime=Date.parse(new Date());
     roleInfo.roleName='123';
     roleInfo.roleLevel='1';
     console.log(roleInfo)
     var missionId='111';
     var missionName='测试开始任务';
     var doMissionTimes=10;
     var roleCurrentPower=1;
     var data={};
     data.roleInfo=roleInfo;
     data.missionId=missionId;
     data.missionName=missionName;
     data.doMissionTimes=doMissionTimes;
     data.roleCurrentPower=roleCurrentPower;
     console.log(data)
     window.XGAndroid.callXGMissionBegin(JSON.stringify(data));
}
```
- **输入数据格式**

```js
{
    "roleInfo": {   //角色信息,参数参考【关于 RoleInfo 的成员说明】
        "uid": "uc_29c4bb6d76924a86c020397c94d2b138",
        "roleId": "10008916",
        "roleType": "create",
        "roleLevel": "1",
        ...
    },
    "missionId": "111", //任务ID
    "missionName": "测试开始任务",   //任务名称
    "doMissionTimes": 10,    //任务执行时间
    "roleCurrentPower": 10  //todo!!!!!
}

```
//todo 为啥不是回调
### 5.4 任务成功
### 5.5 任务失败




### 5.6 购买虚拟货币
- **接口**
**window.XGAndroid.callXGVirtualCurrencyPurchase(data);**

- **接口说明**
> 充值获得的虚拟货币
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
    <button id="btn_Virtual_currency_purchase" onclick="onVirtualCurrencyPurchase()">调用 西瓜SDK 购买虚拟货币【onVirtualCurrencyPurchase】</button>

js代码:

//购买虚拟货币
function onVirtualCurrencyPurchase() {
     var roleInfo={};
     roleInfo.uid='uc_29c4bb6d76924a86c020397c94d2b138';
     roleInfo.serverId='1200';
     roleInfo.serverName='测试123';
     roleInfo.zoneId='123456';
     roleInfo.zoneName='测试124';
     roleInfo.roleId='10008916';
     roleInfo.setRoleCreateTime=Date.parse(new Date());
     roleInfo.roleName='123';
     roleInfo.roleLevel='1';
     console.log(roleInfo)
     var amount=10;
     var virtualCurrencyType='元宝';
     var virtualCurrencyTotal=10;
     var gameTradeNo='123456789';
     var data={};
     data.roleInfo=roleInfo;  //角色信息
     data.amount=amount;  //获得数量
     data.virtualCurrencyType=virtualCurrencyType; //虚拟货币名称，如：元宝、金币等
     data.virtualCurrencyTotal=virtualCurrencyTotal;  //虚拟货币总量,如：100、1000、10000
     data.gameTradeNo=gameTradeNo; //游戏订单号
     console.log(data)
     window.XGAndroid.callXGVirtualCurrencyPurchase(JSON.stringify(data));
}
```
- **输入数据格式**

```js
{
    "roleInfo": {   //角色信息,参数参考【关于 RoleInfo 的成员说明】
        "uid": "uc_29c4bb6d76924a86c020397c94d2b138",
        "roleId": "10008916",
        "roleType": "create",
        "roleLevel": "1",
        ...
    },
    "amount": 10, //获得数量
    "virtualCurrencyType": '元宝',   //虚拟货币名称，如：元宝、金币等
    "virtualCurrencyTotal": 10,    //虚拟货币总量,如：100、1000、10000
    "gameTradeNo": '123456789'  //游戏订单号
}

```
### 5.7 赠送虚拟货币
- **接口**
**window.XGAndroid.callXGVirtualCurrencyReward(data);**

- **接口说明**
> 玩家可以在任务奖励、登录奖励、成就奖励等环节获得赠送的虚拟货币
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
    <button id="btn_virtual_currency_reward" onclick="onVirtualCurrencyReward()">调用 西瓜SDK 赠送虚拟货币 【onVirtualCurrencyReward】</button>

js代码:

//赠送虚拟货币
function onVirtualCurrencyReward() {
     var roleInfo={};
     roleInfo.uid='uc_29c4bb6d76924a86c020397c94d2b138';
     roleInfo.serverId='1200';
     roleInfo.serverName='测试123';
     roleInfo.zoneId='123456';
     roleInfo.zoneName='测试124';
     roleInfo.roleId='10008916';
     roleInfo.setRoleCreateTime=Date.parse(new Date());
     roleInfo.roleName='123';
     roleInfo.roleLevel='1';
     console.log(roleInfo)
     var amount='10';
     var virtualCurrencyType='1';
     var virtualCurrencyTotal=10;
     var gainChannel='抽宝箱';
     var gainChannelType='闯关';
     var gameTradeNo='123456789';
     var data={};
     data.roleInfo=roleInfo;  //角色信息
     data.amount=amount;  //获得数量
     data.virtualCurrencyType=virtualCurrencyType; //虚拟货币名称，如：元宝、金币等
     data.virtualCurrencyTotal=virtualCurrencyTotal;  //虚拟货币总量,如：100、1000、10000
     data.gainChannel=gainChannel; //货币来源，比如（每日登录奖励,抽宝箱等)
     data.gainChannelType=gainChannelType; //货币来源类型比如日常任务、闯关等
     data.gameTradeNo=gameTradeNo; //游戏订单号
     console.log(data)
     window.XGAndroid.callXGVirtualCurrencyReward(JSON.stringify(data));
}
```
- **输入数据格式**

```js
{
    "roleInfo": {   //角色信息,参数参考【关于 RoleInfo 的成员说明】
        "uid": "uc_29c4bb6d76924a86c020397c94d2b138",
        "roleId": "10008916",
        "roleType": "create",
        "roleLevel": "1",
        ...
    },
    "amount": 10, //获得数量
    "virtualCurrencyType": '元宝',   //虚拟货币名称，如：元宝、金币等
    "virtualCurrencyTotal": 10,    //虚拟货币总量,如：100、1000、10000
    "gainChannel": '抽宝箱'    //货币来源，比如（每日登录奖励,抽宝箱等)
    "gainChannelType": '闯关',    //货币来源类型比如日常任务、闯关等
    "gameTradeNo": '123456789'  //游戏订单号
}

```
### 5.8 消费虚拟货币
- **接口**
**window.XGAndroid.callXGVirtualCurrencyConsume(data);**

- **接口说明**
> 通过当前接口，来调用部分 渠道的特殊接口
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
   <button id="btn_virtual_currency_consume" onclick="onVirtualCurrencyConsume()">调用 西瓜SDK 消费虚拟货币【onVirtualCurrencyConsume】</button>

js代码:

//消费虚拟货币
function onVirtualCurrencyConsume() {
     var roleInfo={};
     roleInfo.uid='uc_29c4bb6d76924a86c020397c94d2b138';
     roleInfo.serverId='1200';
     roleInfo.serverName='测试123';
     roleInfo.zoneId='123456';
     roleInfo.zoneName='测试124';
     roleInfo.roleId='10008916';
     roleInfo.setRoleCreateTime=Date.parse(new Date());
     roleInfo.roleName='123';
     roleInfo.roleLevel='1';
     console.log(roleInfo)
     var amount='10';
     var virtualCurrencyType='1';
     var virtualCurrencyTotal=10;
     var itemNum=1;
     var itemName='购买体力';;
     var itemType='道具';
     var data={};
     data.roleInfo=roleInfo;  //角色信息
     data.amount=amount;  //获得数量
     data.virtualCurrencyType=virtualCurrencyType; //虚拟货币名称，如：元宝、金币等
     data.virtualCurrencyTotal=virtualCurrencyTotal;  //虚拟货币总量,如：100、1000、10000
     data.itemNum=itemNum; //消费项目的数量,如1、2、3
     data.itemName=itemName; //消费项目（比如十连抽，购买体力等)
     data.itemType=itemType; //消费类型 比如道具
     console.log(data)
     window.XGAndroid.callXGVirtualCurrencyConsume(JSON.stringify(data));
}

```
- **输入数据格式**

```js
{
    "roleInfo": {   //角色信息,参数参考【关于 RoleInfo 的成员说明】
        "uid": "uc_29c4bb6d76924a86c020397c94d2b138",
        "roleId": "10008916",
        "roleType": "create",
        "roleLevel": "1",
        ...
    },
    "amount": 10, //获得数量
    "virtualCurrencyType": '元宝',   //虚拟货币名称，如：元宝、金币等
    "virtualCurrencyTotal": 10,    //虚拟货币总量,如：100、1000、10000
    "itemNum": 1    //消费项目的数量,如1、2、3
    "itemName": '购买体力',    //消费项目（比如十连抽，购买体力等)
    "itemType":'道具'  //消费类型 比如道具
}

```

## 6.运营活动接口

### 6.1 礼包码兑换，绑定手机号(西瓜提供页面)
- **接口**
**window.XGAndroid.callXGOpenWebActivity(data);**

- **接口说明**
> 开启活动页面
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
   <button id="btn_open_webActivity" onclick="openWebActivity()">调用 西瓜SDK 礼包码兑换，绑定手机号【openWebActivity】</button>

js代码:
//礼包码兑换，绑定手机号
function openWebActivity() {
     var data={};
     data.uid='10';
     data.activityType='ACTIVITY_TYPE_GIFT';;
     data.roleId='123';
     data.zoneId='123';
     data.serverId='123';
     console.log(data)
     window.XGAndroid.callXGOpenWebActivity(JSON.stringify(data));
}

```
- **输入数据格式**

```js
{
    "uid": '123',   //玩家uid
    "activityType": 'ACTIVITY_TYPE_GIFT',  //活动类型（ACTIVITY_TYPE_GIFT/ACTIVITY_TYPE_MOBILE_BIND分别为兑换礼包码和绑定手机号）
    "roleId": '123'   //玩家角色ID
    "zoneId": '123',    //游戏区ID
    "serverId":'123'  //游戏服ID
}

```
### 6.2 礼包码兑换 （游戏提供界面）
- **接口**
**window.XGAndroid.callXGExchangeGiftCode(data);**

- **接口说明**
> 礼包码兑换
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
   <button id="btn_exchange_giftCode" onclick="exchangeGiftCode()">调用 西瓜SDK 礼包码兑换(游戏提供界面)，绑定手机号【exchangeGiftCode】</button>

js代码:
//礼包码兑换 （游戏提供界面）
function exchangeGiftCode() {
     var data={};
     data.uid='10';
     data.roleId='123';
     data.zoneId='123';
     data.serverId='123';
     data.giftCode='123';
     console.log(data)
     window.XGAndroid.callXGExchangeGiftCode(JSON.stringify(data));
}

```
- **输入数据格式**

```js
{
    "uid": '123',   //玩家uid
    "roleId": '123'   //玩家角色ID
    "zoneId": '123',    //游戏区ID
    "serverId":'123',  //游戏服ID
    "giftCode":'123'  //礼包码
}

```
### 6.3 礼包码兑换 （游戏提供界面）回调
- **接口**
**function onExchangeGiftCodeFinish(data)**

- **接口说明**
> 礼包码兑换结束后调用
   
- **代码**

```js
function onXGExchangeGiftCodeFinish(data) {
    document.getElementById("log_msg").innerHTML = ("onXGExchangeGiftCodeFinish... " + data);
}
```
- **输出数据格式**

```js
{
"code": 10001,  //返回码
"msg": "xxx",    //返回信息
}
```

### 6.4 绑定手机号（游戏提供界面）
#### 6.4.1 获取验证码
- **接口**
**window.XGAndroid.callXGSendCaptcha(data);**

- **接口说明**
> 礼包码兑换
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
  <button id="btn_send_captcha" onclick="sendCaptcha()">调用 西瓜SDK 绑定手机号,发送验证码【sendCaptcha】</button>

js代码:
//发送验证码
function sendCaptcha() {
var data={};
     data.mobile='131256454878';
     data.uid='uc_29c4bb6d76924a86c020397c94d2b138';
     data.serverId='123';
     data.zoneId='123';
     data.roleId='123';
     data.roleName='测试1';
     window.XGAndroid.callXGSendCaptcha(JSON.stringify(data));
}

```
- **输入数据格式**

```js
{   
    "mobile": '131256454878',   //手机号
    "uid": 'uc_29c4bb6d76924a86c020397c94d2b138',   //玩家uid
    "roleId": '123'   //玩家角色ID
    "zoneId": '123',    //游戏区ID
    "serverId":'123',  //游戏服ID
    "roleName":'测试1'  //角色名
}

```

#### 6.4.2 获取验证码回调
- **接口**
**function onXGSendCaptchaFinish(data)**

- **接口说明**
> 发送验证码结束后回调
   
- **代码**

```js
function onXGSendCaptchaFinish(data) {
    document.getElementById("log_msg").innerHTML = ("onXGSendCaptchaFinish..." + data);
}
```
- **输出数据格式**

```js
{
"code": 10001,  //返回码
"msg": "xxx",    //返回信息
}
```

#### 6.4.3 绑定手机号 
- **接口**
**window.XGAndroid.callXGBindMobile(data)**
- **接口说明**
> 绑定手机号
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
 <button id="btn_bind_mobile" onclick="bindMobile()">调用 西瓜SDK 绑定手机号【bindMobile】</button>
 
 js代码:
//绑定手机号
function bindMobile() {
var bindMobileInfo={};
     var mobile='131412221332';
     var uid='uc_29c4bb6d76924a86c020397c94d2b138';
     var roleId='12345';
     var zoneId='12345';
     var serverId='123';
     var roleName='小米';
     var captcha='12345'
     var data={};
     data.bindMobileInfo=bindMobileInfo;
     data.captcha=captcha;;
     console.log(data)
     window.XGAndroid.callXGBindMobile(JSON.stringify(data));
}

```
- **输入数据格式**

```js
{
    "bindMobileInfo": { //参考【关于 BindMobileInfo 的成员说明】
        "mobile": "131412221332",
        "uid": "uc_29c4bb6d76924a86c020397c94d2b138",
        "serverId": "123",
        "zoneId": "12345",
        "roleId": "12345",
        "roleName": "小米"
    },
    "captcha": "12345" //接收到的手机验证码
}

```
- **关于 BindMobileInfo 的成员说明**

**所有必字段必须进行接入！**

|  参数 |  参数类型 | 最大长度| 说明  |  必须 |
| :------------ | :------------: | :------------: | :------------ | :------------: |
| mobile | string | 11 | 手机号 |Y |
| uid | string | 128 | 用户ID,游戏必须使用登录时西瓜服务器返回的uid |Y |
| serverId | string | 32 | 游戏服ID |Y |
| zoneId | string | 32 | 区ID |Y |
| roleId | string | 32 | 角色ID |Y |
| roleName | string | 64 | 角色名 |Y |


#### 6.4.4 绑定手机号回调
- **接口**
**function onXGBindMobileFinish(data)**

- **接口说明**
> 绑定手机号后回调
   
- **代码**

```js
function onXGBindMobileFinish(data) {
    document.getElementById("log_msg").innerHTML = ("onXGBindMobileFinish..." + data);
}
```
- **输出数据格式**

```js
{
"code": 10001,  //返回码
"msg": "xxx",    //返回信息
}
```
### 6.4 问卷调查（游戏提供界面）
**问卷的内容和完成问卷返回的礼品信息，需要联系西瓜数据和运营人员设定完成。**
#### 6.4.1 初始化问卷
##### 6.4.1.1 问卷状态更新后回调
- **接口**
**function onXGInitQuestionnaire(questionnaireName)**

- **接口说明**
> -  问卷状态更新后，用该方法处理问卷信息的显示与通知
> -  在进入游戏，或完成问卷，或主动调用问卷刷新接口时触发
   
- **代码**

```js
function onXGInitQuestionnaire(data) {
    document.getElementById("log_msg").innerHTML = ("onXGInitQuestionnaire...questionnaireName =" + questionnaireName);
}
```
- **输出数据格式**

```js
questionnaireName
```

##### 6.4.1.2 问卷完成后回调
- **接口**
**function onXGFinishQuestionnaire(giftInfo)**

- **接口说明**
> 问卷完成后，用该方法处理完成问卷的相关奖励。
   
- **代码**

```js
function onXGFinishQuestionnaire(giftInfo) {
    document.getElementById("log_msg").innerHTML = ("onXGFinishQuestionnaire...giftInfo = " + giftInfo);
}
```
- **输出数据格式**

```js
giftInfo
```

#### 6.4.2 刷新问卷
- **接口**
**window.XGAndroid.callXGRefreshQuestionnaire(data)**
- **接口说明**
> 游戏初始化问卷后手动调用刷新问卷，查看问卷是否更新。
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
 <button id="btn_refresh_questionnaire" onclick="refreshQuestionnaire()">调用 西瓜SDK 刷新问卷【refreshQuestionnaire】</button>
 
 js代码:
function refreshQuestionnaire() {
    var roleInfo={};
       roleInfo.uid='uc_29c4bb6d76924a86c020397c94d2b138';
       roleInfo.serverId='1200';
       roleInfo.serverName='测试123';
       roleInfo.zoneId='123456';
       roleInfo.zoneName='测试124';
       roleInfo.roleId='10008916';
       roleInfo.setRoleCreateTime=Date.parse(new Date());
       roleInfo.roleName='123';
       roleInfo.roleLevel='1';

       var missionId='111';
       var missionName='刷新问卷';

       var data={};
       data.roleInfo=roleInfo;  //对象信息
       data.missionId=missionId;  //任务ID
       data.missionName=missionName; //任务名称

       console.log(data)
       window.XGAndroid.callXGRefreshQuestionnaire(JSON.stringify(data));
}

```
- **输入数据格式**

```js
{
    "roleInfo": {   //角色信息,参数参考【关于 RoleInfo 的成员说明】
        "uid": "uc_29c4bb6d76924a86c020397c94d2b138",
        "roleId": "10008916",
        "roleType": "create",
        "roleLevel": "1",
        ...
    },
    "missionId": "111", //任务ID 可为空
    "missionName": "刷新问卷" //任务名称 可为空
}

```

#### 6.4.3 打开问卷
- **接口**
**window.XGAndroid.callXGOpenQuestionnaire(data)**
- **接口说明**
> 当游戏有通过游戏用户在线分发问卷的需求时，可以通过本SDK的接入简化开发提高效率节省成本
- **参数说明**
>  参考下方【输入数据格式】
- **代码**

```js
html代码:
 <button id="btn_open_questionnaire" onclick="openQuestionnaire()">调用 西瓜SDK 打开问卷【openQuestionnaire】</button>
 
 js代码:
function openQuestionnaire() {
    var info={}
    info.width=80;
    info.height=80;
    window.XGAndroid.callXGOpenQuestionnaire(JSON.stringify(info));
}

```
- **输入数据格式**

```js
{
    "width": 80, //打开问卷窗口的宽度占屏幕的百分比，100表示全屏
    "height": 80 //打开问卷窗口的高度占屏幕的百分比，100表示全屏
}

```

## 7.渠道接入要点须知

- **华为：**
   -  要求传入的productDesc非空，不能包含特殊字符，包括 # " & / ? $ ^ *:) \ < > | , = 回车 换行，否则会导致无法拉起支付
<p>

- **快发：**
  - 要求首次启动游戏onCreateRole的信息和onEnterGame的一致
<p>

- **UC：**
   - 角色创建时间为必传

  - zoneName要与角色进入游戏时，玩家看到的信息相同，如：界面显示（一区 桃园结义），zoneName也必须传（一区 桃园结义）
<p>

- **应用宝：**
   - 调用西瓜login接口可以传参：{\"platform\":\"qq\"} or {\"platform\":\"weixin\"}"

   - serverid必须为纯数字，且不能超过2147483647

## 8.错误码表及常见错误

错误码值| 错误码说明 |
---|---|
200|成功
1000| 客户端初始化失败 |
1100| 客户端登录失败 |
1200| 客户端切换账号失败 |
1300| 客户端登出失败 |
1400| 客户端退出失败 |
1500| 登录失败，渠道正在初始化 |
2000| 支付失败 |
2010| 创建订单失败 |
2020| 订单金额错误 |
2021| 货币错误（iOS用）|
2030| UID错误 |
2040| 产品数量错误 |
2050| 扩展信息错误 |
2060| 渠道反馈的支付失败 |
2070| 短时间内重复支付（2秒内）|
2080| 正在支付中 |
2090| 支付结果未知 |
2100| 支付取消 |



