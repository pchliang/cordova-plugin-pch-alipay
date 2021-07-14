# cordova-plugin-pch-alipay
### 前言：
cordova-plugin-pch-alipay插件是在[cordova-plugin-gubnoi-alipay](https://github.com/jing-zhou/cordova-plugin-alipay)插件的基础上修改过来的。由于原插件已经很长时间没有跟进更新了，虽然安卓端的功能都能正常使用，但是ios端存在不少问题需要跟进更新，本插件主要是为了处理原插件存在的问题以及更新最新的SDK包，在插件安装和使用上跟原插件保持一致。
###### 本插件仅支持《APP支付》，不支持移动支付
***
### 主要修复的BUG(2021-07-13)
1. （仅ios端）修复Alipay.m文件报错: 'Alipay.h' flie not found.，导致的无法编译；
2. （仅ios端）修复Alipay.m文件报错: No known class method for selector 'initWithStatus:message:'，导致的无法编译；
3. （仅ios端）修复调起支付时报错: ERROR: Plugin 'Alipay' not found, or is not a CDVplugin. Check your mapping in config.xml 导致的无法调起支付问题；
4. （仅ios端）修复支付成功后或取消支付后，无法返回到原应用的问题。

***
### SDK更新
2021-07-13从官网下载最新SDK
android包从原来的jar, 改为aar方便日后更新

***
### 支持平台
1. android
2. iOS
##### note：xcode版本须大于7.0

***
### 安装
###### 在线安装
    cordova plugin add cordova-plugin-pch-alipay --variable APP_ID=[your AppId]

###### 本地安装
下载插件到本地

    cordova plugin add /your/local/path --variable APP_ID=[your AppId]
    
***
### 使用 API

    //订单在服务端签名生成订单信息，具体请参考官网进行签名处理[支付宝官网文档](https://docs.open.alipay.com/204/105465)

    var payInfo = "订单信息";  
    cordova.plugins.ali.Alipay.pay(payInfo,function success(e){},function error(e){});
    //e.resultStatus  状态代码  e.result  本次操作返回的结果数据 e.memo 提示信息
    //e.resultStatus  9000  订单支付成功 ;8000 正在处理中  调用function success
    //e.resultStatus  4000  订单支付失败 ;6001  用户中途取消 ;6002 网络连接出错  调用function error
    //当e.resultStatus为9000时，请去服务端验证支付结果
    
    /**
    * 同步返回的结果必须放置到服务端进行验证（验证的规则请看https://doc.open.alipay.com/doc2/detail.htm?spm=0.0.0.0.xdvAU6&treeId=59&articleId=103665&docType=1) 建议商户依赖异步通知
    */

