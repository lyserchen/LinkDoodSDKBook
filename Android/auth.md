##认证 

```java
Auth auth= SDKClient.instance().getAuth()
```
###注册
    注册账号分为三步，获取验证码，校验验证码，设置密码。

####获取验证码：
传入参数：（手机号，服务器，国家码，ResultCallBack<Long>）
callBack成功返回 注册ID（验证注册码时需要）
``` java
auth.register(String user, String entArea, String nationalCode, ResultCallBack<Long> callBack);
```
####校验验证码：
传入参数：（注册ID，注册验证码，ResultCallBack）
callBack返回成功进入下一步 registerStep
```java
auth.registerVerify(long registerID, String code, ResultCallBack callBack);
```
####设置密码：
传入参数：（注册ID，姓名，密码，ResultCallBack）
callBack返回成功表示注册成功，注册完成
```java 
auth.registerStep(long registerID, String name, String password, ResultCallBack callBack);
```
###登录
####获取预登录服务器状态
传入参数：（企业域）
直接返回LoginExtraInfo
```java 
LoginExtraInfo extraInfo = auth.getPreLoginInfo(String serverName);
```
####手动登录
传入参数：（账号，密码，企业域，国家码，ResultcallBack）
callBack返回code=117或者1102需要调用进行验证码验证
```java 
auth.login(String account, String password, String entArea, String nationalCode, ResultCallBack callBack);
```
####获取登录验证码
登录返回 code=117或者1102时调用此方法显示登录验证码
```java 
auth.getVerifyImgUrl()
```
####登录验证码验证
传入参数：（是否为获取下一张验证码，用户名，验证码，ResultCallBack）
```java 
 auth.loginVerify(boolean next, String userName, String code, ResultCallBack callBack)
```
###自动登录
单个账号或者上次登录主账号在登录前判断是否可以自动登录
```java 
boolean autoLogin = auth.isAutoLogin()
```
单个账号或者上次登录主账号 执行自动登录
```java 
auth.autoLogin(ResultCallBack callBack);
```
多个账号自动登录
传入参数：（用户ID，服务器地址，callBack）
```java 
auth.autoLogin(long userID,String entArea,ResultCallBack callBack);
```
### 退出
单个账号退出或者主账号退出调用，子账号退出调用AccountService.logout
```java 
auth.logout(ResultCallBack callBack);
```
###忘记密码
 忘记密码分为三步，获取验证码，校验验证码，设置新密码。

####获取验证码：
传入参数：（手机号，服务器，国家码，ResultCallBack<Long>）
callBack成功返回 验证码ID（验证时需要）
```java 
auth.forgetPassword(String user, String entArea, String nationalCode, ResultCallBack<Long> callBack)；
```
####校验验证码：
传入参数：（验证ID，验证码，ResultCallBack）
callBack返回成功进入下一步
```java 
auth.forgetPasswordVerify(long registerID, String code, ResultCallBack callBack);
```
####设置密码：
传入参数：（注册ID，密码，ResultCallBack）
```java 
auth.forgerPasswordStep(long registerID, String password, ResultCallBack callBack);
```
###获取密码规则
```java 
auth.getPasswordRule(ResultCallBack<Integer> callBack);
```
###修改密码（登录成功后使用）
```java 
modifyPassword(String original, String newPassword, ResultCallBack callBack);
```
###获取安全中心页面
传入参数:（ 服务器名称，客户端版本号，callBack）

```java 
auth.getSecUrl(String entArea, String version, ResultCallBack<String> callBack)
```
###获取登录服务器时间
```java 
auth.getServerTime(ResultCallBack<Long> callBack)
```
###找回隐藏密码
```java 
auth.verifyHiddenInfo(ArrayList<HiddenAccountInfoBean> list, ResultCallBack<HiddenAccountInfoResult> callBack)
```
###重置隐藏密码
```java 
auth.resetHiddenPWD(String oldPwd, String newPwd, ResultCallBack callBack) 
```
###设置用户自身配置
```java 
/**
     * 设置用户自身配置
     * 其中包含：生日，电话，邮件，好友，Ｖ标，提醒模式，全局消息通知模式
     *  PersonalDataBean设置
     * type:   1 (生日)，２（电话），３（邮件）
     * 　　　　　　　　value:  1：所有人可见 2：仅好友可见 3：仅自己可见，默认1
     * type:   4 (好友验证方式)
     * 　　　　　　　 value:   1：需要验证信息,2:不允许任何人添加,3:允许任何人添加，默认1
     * type:   5 V标
     * value: 1:表示始终有声音提醒，2：表示始终无声音提醒 3:不始终提醒，默认1
     * type:   6 @相关人提醒模式
     * value: 1:表示始终有声音提醒，2：表示始终无声音提醒 3:不始终提醒，默认1
     * type:   7 全局通知消息内容展现模式
     * value: 1:通知详情，2：通知源，隐藏内容 3:完全隐藏，默认2
     * @param item     用户设置，如果是单条修改，成功 返回 1，失败 返回 0 ；如果多条修改，则返回修改成功的条数
     * @param callBack 返回修改成功的条数
     * @return
     */
auth.setPersonalData(ArrayList<PersonalDataBean> item, ResultCallBack<Integer> callBack) 
```
###获取用户自身配置
```java 
/**
* 需要获取那些类型的数据，把类型添加进列表,要获取全部的话，列表可置为空。
*/
auth.getPersonalData(ArrayList<PersonalDataBean> item, ResultCallBack<ArrayList<PersonalDataBean>> callBack)
```
###特定用户信息设置
```java 
    /**
     * type = 1: 设置是否显示在线信息 flag: 0显示 1不显示 默认0
     * type = 3: 设置豆豆号查找 flag: 0允许 1不允许 默认0
     * type = 4: 设置手机号查找 flag: 0允许 1不允许 默认0
     * type = 5: 设置邮箱号查找 flag: 0允许 1不允许 默认0
     * type = 6: 设置分享更新   flag: 0提示更新 1不提示更新 默认0
     * type = 7: 新消息通知是否提醒 flag: 0提醒 1不提醒 默认0
     * type = 12: 多服务新消息通知是否提醒 flag: 0不始终提示 1始终提示 默认0
     * type = 13: 多服务设置V标好友始终提醒 flag: 0不始终提示 1始终提示 默认0
     * type = 14: 多服务设置设置@相关人始终提醒 flag: 0不始终提示 1始终提示 默认0
     */
    auth.setUserSetting(int type, byte flag, ResultCallBack callBack) 
```
###得到特定用户信息设置
```java 
    /**
     * type = 0: 返回所有结果，保存在long中，其中每个设置所在的位置与type一致 如 00000000000100 第三位等于1  代表 不允许通过豆豆的号查找
     * type = 1: 获取否显示在线信息 flag: 0显示 1不显示 默认0
     * type = 3: 获取豆豆号查找 flag: 0允许 1不允许 默认0
     * type = 4: 获取手机号查找 flag: 0允许 1不允许 默认0
     * type = 5: 获取邮箱号查找 flag: 0允许 1不允许 默认0
     * type = 6: 获取分享更新   flag: 0提示更新 1不提示更新 默认0
     * type = 7: 新消息通知是否提醒 flag: 0提醒 1不提醒 默认0
     * type = 12: 多服务新消息通知是否提醒 flag: 0不始终提示 1始终提示 默认0
     * type = 13: 多服务V标好友始终提醒 flag: 0不始终提示 1始终提示 默认0
     * type = 14: 多服务@相关人始终提醒 flag: 0不始终提示 1始终提示 默认0
     */
    auth.getUserSetting(int type, ResultCallBack<Long> callBack) 
```
###解析GetUserSetting返回结果
传入参数：（解析type,获取到的setting result）
返回结果：false:0 ,true:1
```java 
boolean verify = auth.verifyUserSetting(int type ,long result)
```
###本地与用户相关的配置存储，只有登录后才能使用
```java 
 /**
 * LocalSettingBean参数：
 *  type 的值不同，items有不同的意义
 * 	0: items里面是新插入的值
 * 	1: items里面带要查询的值，st_localSetting只给key赋值即可
 * 	2: items带最新的值
 * 	3: items里面带要删除的值，st_localSetting只给key赋值即可
 */
auth.localSetting(byte type, ArrayList<LocalSettingBean> item, ResultCallBack<LocalSettingResult> callBack) 
```

##账户管理 
```java
AccountService accountService = SDKClient.instance().getAccountService()
```

###获取当前登录账户

```java
Account current = accountService.getCurrent()
``` 
###当前账户ID

```java
long userID = accountService.getUserID();
```
###判断是否为当前账户
```java 
boolean isMyself = accountService.isMyself(long userID);
```

###添加子账户
设置后台子账户个数,默认最大数为4个
```java 
accoutService.setMax(int max);
```
分为两步：
注意：客户端在认为添加账号结束时必须调用添加完成或者取消
添加准备
```java 
accountService.addPrepare();
```
添加完成
```java 
accountService.addFinish(long userID);
```
取消
```java
accountService.addCancel();
```
###切换账号
```java 
accountService.switchOver(long userID);
```
###退出子账号
```java 
accountService.logout(long userID)；
```
###设置子帐号消息监听
```java 
accountService.setNewMsgListener(NewMsgListener listener);
```
###获取当前账号绑定的子账号，注：登录成功后需要客户端自己调用添加子账号流程，执行自动登录接口登录子账号
```java 
ArrayList<ServerInfo> list = accountService.getBindServer();
```
###刷新后台子账号消息，注：刷新机制客户端处理，刷新时间间隔需大于2分钟
```java 
accountService.refreshMsg(long userID);
```
###设置是否推送后台子账号消息
```java 
accountService.setNotifyMsg(long userID, boolean notify);
```
###后台子账号消息接收监听
```java 
accountService.setNewMsgListener(new NewMsgListener(){
    @Override
    public void onReceive(long userID,Chat chat){
          //Todo 根据userID判断是哪个账户的消息
    }
});
```

###个人信息
```java
Account current = accountService.getCurrent();
```
#### 个人信息
```java 
Contact myInfo = current.getMyInfo();
```
####判断当前账户在线
判断是否已经登录成功在线

```java 
boolean online = current.isOnline();
```
####设置个人信息（不包括设置头像）
修改个人信息，修改头像调用其它方法
传入参数：（修改信息Contact，callBack）
说明示例

```java 
Contact contact = new Contact();
//仅修改名称,不需要修改的不用设置
contact.setName("name");
current.updateInfo(contact,callBack);
current.updateInfo(Contact myInfo, ResultCallBack callBack);
```
###设置个人头像
传入参数：（头像本地路径，callBack)

```java
auth.setAvater(String avatar,ResultCallBack callBack);
```
####设置个人信息更改监听
修改个人信息成功后通过推送更新信息

```java
current.setInfoChangeListener(InfoChangeListener listener);
```
####设置重登录监听
账户被踢或者session过期会导致账户需要重新登录

```java
current.setReLoginListener(ReLoginListener listener)
```
####设置数据更新监听
SDK版本更新时可能会出现数据库更新操作，需要在界面上等待更新完成后执行其他操作

```java
current.setDbUpdateListener(DBUpdateListener listener);
```

##企业组织 
```java
EnterpriseService enterpriseService = SDKClient.instance().getEnterpriseService()
```
###获取企业
```java
enterpriseService.getEntList(ResultCallBack<ArrayList<EnerpriseBean>> callBack);
```
###获取组织成员列表
传入参数：（企业id，组织id ，callBak）
企业根组织第一次获取传（0，0）
组织ID在第一次取得时候传0，之后传入要获取的组织ID
返回结果：回调中返回组织和成员列表

```java
enterpriseService.getOrgAndUserList(long enterpriseID,long organizeID,ResultCallBack<OrgAndUserListResult> callBack)
```