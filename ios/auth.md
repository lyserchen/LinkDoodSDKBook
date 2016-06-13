##认证
###登录
####手动登录
```
/*!

* @method    loginWithAccount-登录

* @descript  全局登录接口

* @param     account   登录帐号

* @param     passwor   登录密码

* @param     loginType  登录类型

* @param     region  国家或者地区编码

* @param     domain  服务器标识或者服务器地址

* @param     completion  登录结果(error为空表示成功,失败有具体失败原因说明)

* @result    空

*/

- (void)loginWithAccount:(NSString*)account

                password:(NSString*)pwd

               loginType:(login_type)loginType

                  region:(NSString*)regionCode

                  domain:(NSString *)domain

              completion:(void (^) (NSError *error))completion;
```

####通过密码验证历史账号登录
```
/*!

* @method    loginWithAccount-登录

* @descript  全局登录接口

* @param     password  登录密码

* @param     completion  登录结果(error为空表示成功,失败有具体失败原因说明)

* @result    空

*/

- (void)autoLoginWithPassword:(NSString*)password

       	completion:(void (^) (NSError *error))completion;
```

####自动登录
利用历史账号登录，登录结果（error为空表示成功，失败有具体失败原因说明）

	- (void)autoLogin:(void (^) (NSError *error))completion;
####登出
退出登录,登录接口回调代码块

	- (void)logoff:(void (^)(NSError *error))completion;
###应用授权
授权第三方应用key

	- (void)clientKey:(void (^) (NSError *error,NSString *clientKey))completion;	
###其他功能或信息获取
获取服务器时间

	- (void)serverTime:(void (^) (NSError *error,int64_t time))completion;
通过注册apns推送获取到的设备标识

	- (void)registerPushToken:(NSString*)pushToken completion:(void (^) (NSError *error))completion;
账号激活状态（打开或者关闭notify消息,用于多服务器子账号或者主账号程序运行状态切换），设置是否成功

	- (bool)makeActivationState:(active_state)state;
###注册、找回密码
注册第一步，获取验证码和注册标识

	- (void) registery1:(void (^) (bool state,NSDictionary *object))completion;
注册第二步，设置昵称和密码

	- (void) registery2:(void (^)(bool, NSDictionary *))completion;
找回密码第一步，同注册第一步

	- (void) resetPwd1:(void (^) (bool state,NSDictionary *object))completion;
找回密码第二部，设置新的密码

	- (void) resetPwd2:(void (^)(bool, NSDictionary *))completion;
##全局运行数据
获取SDK版本号

	- (NSString*)version;
**通过证书注册应用（必须注册应用才能使用SDK）**

```
/*!

* @method    registerApp

* @descript  通过证书注册应用(必须注册应用才能正常使用sdk)

* @param     certificatePath   证书地址

* @param     cacheFolder       缓存保存地址

* @result    初始化后的缓存地址

*/

- (NSString*)registerApp:(NSString*)certificatePath onCachePath:(NSString*)path;

```


	
		
	   