##账户管理 
`AccountService accountService = SDKClient.instance().getAccountService()`

###获取当前登录账户
``` 
Account current = accountService.getCurrent()
``` 
###当前账户ID
``` 
long userID = accountService.getUserID();
```
###判断是否为当前账户
``` 
boolean isMyself = accountService.isMyself(long userID);
```

###添加子账户
设置后台子账户个数,默认最大数为4个
``` 
accoutService.setMax(int max);
```
分为两步：
注意：客户端在认为添加账号结束时必须调用添加完成或者取消
添加准备
``` 
accountService.addPrepare();
```
添加完成
``` 
accountService.addFinish(long userID);
```
取消
``` 
accountService.addCancel();
```
###切换账号
``` 
accountService.switchOver(long userID);
```
###退出子账号
``` 
accountService.logout(long userID)；
```
###设置子帐号消息监听
``` 
accountService.setNewMsgListener(NewMsgListener listener);
```
###获取当前账号绑定的子账号，注：登录成功后需要客户端自己调用添加子账号流程，执行自动登录接口登录子账号
``` 
ArrayList<ServerInfo> list = accountService.getBindServer();
```
###刷新后台子账号消息，注：刷新机制客户端处理，刷新时间间隔需大于2分钟
``` 
accountService.refreshMsg(long userID);
```
###设置是否推送后台子账号消息
``` 
accountService.setNotifyMsg(long userID, boolean notify);
```
###后台子账号消息接收监听
``` 
accountService.setNewMsgListener(new NewMsgListener(){
    @Override
    public void onReceive(long userID,Chat chat){
          //Todo 根据userID判断是哪个账户的消息
    }
});
```

###个人信息
`Account current = accountService.getCurrent();`
#### 个人信息
``` 
Contact myInfo = current.getMyInfo();
```
####判断当前账户在线
判断是否已经登录成功在线
``` 
boolean online = current.isOnline();
```
####设置个人信息（不包括设置头像）
修改个人信息，修改头像调用其它方法
传入参数：（修改信息Contact，callBack）
说明示例
``` 
Contact contact = new Contact();
//仅修改名称,不需要修改的不用设置
contact.setName("name");
current.updateInfo(contact,callBack);
```
``` 
current.updateInfo(Contact myInfo, ResultCallBack callBack);
```
###设置个人头像
传入参数：（头像本地路径，callBack)
```
auth.setAvater(String avatar,ResultCallBack callBack);
```
####设置个人信息更改监听
修改个人信息成功后通过推送更新信息
```
current.setInfoChangeListener(InfoChangeListener listener);
```
####设置重登录监听
账户被踢或者session过期会导致账户需要重新登录
```
current.setReLoginListener(ReLoginListener listener)
```
####设置数据更新监听
SDK版本更新时可能会出现数据库更新操作，需要在界面上等待更新完成后执行其他操作
```
current.setDbUpdateListener(DBUpdateListener listener);
```