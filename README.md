# cordova-plugin-getuisdk
##安装cordova环境
* 安装cordova 
```
npm install -g cordova
```
* 安装plugman
```
npm install -g plugman
```
* 创建cordova工程
```
cordova create 目录名 应用包名 工程名
```
## Android平台支持
* 添加android平台
```
cordova platform add android
```
* 添加个推推送
```	
plugman install --platform android --project android平台目录 --plugin https://github.com/GetuiLaboratory/cordova-plugin-getuisdk --plugins_dir 你的插件目录 --variable PUSH_APPID=你的appid --variable PUSH_APPKEY=你的appkey --variable PUSH_APPSECRET=你的appsecret
```	
* 安装之后需要重新构建工程
```
cordova build
```
* JS文件中进行个推初始化

##### 回调函数
```
function callback(type, data) {
	if(type == 'cid') {
		//TODO data = clientid
	} else if(type == 'pid') {
		//TODO data = 进程pid
	} else if(type == 'payload') {
   	//TODO data=透传数据
	} else if(type == 'online') {
		if(data == 'true') {
			//TODO 已上线
		$('#clientid').text(clientid);
		} else {
			//TODO 已离线
		}
	}
};
```
##### 初始化插件
```
 GeTuiSdkPlugin.callback_init(callback);   
 GeTuiSdkPlugin.initialize();
```

## iOS平台支持
* 添加ios平台
```
cordova platform add ios
```
* 添加个推推送
```	
plugman install --platform ios --project ios平台目录 --plugin https://github.com/GetuiLaboratory/cordova-plugin-getuisdk --plugins_dir 你的插件目录
```	
* 安装之后需要重新构建工程
```
cordova build
```
* JS文件中进行个推初始化
	
##### 回调函数
```
//clinetid返回
function onRegisterClient(clientId) {
	//TODO clientId = clinetid   
}；

//透传数据返回
function onReceivePayload(payloadId, taskId, msgId, offLine, appId) {
     //TODO playload = 透传数据
	 //TODO taskId = 推送消息的任务id
	 //TODO msgId = 推送消息的messageid
	 //TODO offLine = 是否是离线消息，YES.是离线消息
	 //TODO appId = 应用的appId

};

//发送上行消息返回
function onSendMessage(messageId, result) {
	//TODO messageid = 发送上行消息id
	//TODO result = 发送结果
}；

//SDK内部发生错误返回
function onOccurError(err) {
	//TODO err = 错误信息
};

//sdk状态返回
function onNotifySdkState(status) {
	var callback = function(status) {
        	switch (status) {
        		case GeTuiSdk.GeTuiSdkStatus.KSdkStatusStarting:
                   		//TODO 正在启动
                   	break;
               		case GeTuiSdk.GeTuiSdkStatus.KSdkStatusStarted:
                		//TODO 已经启动
                	break;
			case GeTuiSdk.GeTuiSdkStatus.KSdkStatusStoped:
				//TODO 已经停止
                   	break;
			default:
			break;
		}
	};
	GeTuiSdk.status(callback);
}；

//SDK设置关闭推送模式回调
function onSetPushMode(isModeOff, err) {
	if (err != null) {
		//TODO 设置关闭模式失败
	} else {
		//TODO 设置关闭模式成功
	}
};
```
##### 初始化插件
```
GeTuiSdk.setGeTuiSdkDidRegisterClientCallback(onRegisterClient);
GeTuiSdk.setGeTuiSdkDidReceivePayloadCallback(onReceivePayload);
GeTuiSdk.setGeTuiSdkDidSendMessageCallback(onSendMessage);
GeTuiSdk.setGeTuiSdkDidOccurErrorCallback(onOccurError);
GeTuiSdk.setGeTuiSDkDidNotifySdkStateCallback(onNotifySdkState);
GeTuiSdk.setGeTuiSdkDidSetPushModeCallback(onSetPushMode);
//个推平台申请的参数KAppId, KAppKey, KAppSecret
GeTuiSdk.startSdkWithAppId(KAppId, KAppKey, KAppSecret);
```
## 参考文档
[cordova常用命令](http://my.oschina.net/jack088/blog/390876?fromerr=f8h2gkFq)  

[plugman使用](http://cordova.apache.org/docs/en/latest/plugin_ref/plugman.html)  

[个推官方文档](http://docs.getui.com/pages/viewpage.action?pageId=589866)
