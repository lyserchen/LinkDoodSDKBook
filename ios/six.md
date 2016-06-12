##部分接口(详细接口使用方法请参考API文档)
###认证模块(登录)
####手动登陆(V1.5.0从LDAuthModel迁移到LDClient)

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



####通过密码验证历史账号登录(V1.5.0从LDAuthModel迁移到LDClient)

/*!

* @method    loginWithAccount-登录

* @descript  全局登录接口

* @param     password  登录密码

* @param     completion  登录结果(error为空表示成功,失败有具体失败原因说明)

* @result    空

*/

- (void)autoLoginWithPassword:(NSString*)password

       	completion:(void (^) (NSError *error))completion;



####自动登陆(V1.5.0从LDAuthModel迁移到LDClient)

/*!

* @method    autoLogin

* @descript  利用历史登录帐号登录

* @param     completion

             登录结果(error为空表示成功,失败有具体失败原因说明)

* @result    空

*/

- (void)autoLogin:(void (^) (NSError *error))completion;



####登出

/*!

@delegate  logoff

@descript  退出登录

@param     completion-登录接口回调代码块

@result    空

*/

- (void)logoff:(void (^)(NSError *error))completion;

```

###认证模块(应用授权)

```objectivec

/*!

* @method    clientKey

* @descript  授权第三方应用key

* @param     completion    授权第三方应用key接口回调代码块

* @result    空

*/

- (void)clientKey:(void (^) (NSError *error,NSString *clientKey))completion;

```

###认证模块(其他功能或信息获取)

```objectivec

/*!

* @method    serverTime

* @descript  获取服务器时间

* @param     completion    获取服务器时间接口回调代码块

* @result    空

*/

- (void)serverTime:(void (^) (NSError *error,int64_t time))completion;



/*!

* @method    registerPushToken

* @descript  注册推送通知

* @param     pushToken     通过注册apns推送获取到的设备标识

* @param     completion    注册推送通知接口回调代码块

* @result    空

*/

- (void)registerPushToken:(NSString*)pushToken completion:(void (^) (NSError *error))completion;



/*!

* @method    makeActivationState

* @descript  账号激活状态(打开或者关闭notify消息,用于多服务器子账号或者主账号程序运行状态切换)

* @param     state 状态notify状态 0代表关闭，１代表打开

* @result    是否设置成功

*/

- (bool)makeActivationState:(active_state)state;

```

###认证模块(注册、找回密码)

```objectivec

/*!

@method  registery1

@descript  注册第一步,获取验证码和注册标识

@param     completion-回调代码块

@result    空

*/

- (void) registery1:(void (^) (bool state,NSDictionary *object))completion;



/*!

@method  registery2

@descript  注册第二步,设置昵称和密码

@param     completion-回调代码块

@result    空

*/

- (void) registery2:(void (^)(bool, NSDictionary *))completion;



/*!

@method  resetPwd1

@descript  找回密码第一步,同注册第一步

@param     completion-回调代码块

@result    空

*/

- (void) resetPwd1:(void (^) (bool state,NSDictionary *object))completion;



/*!

@method  resetPwd2

@descript  找回密码第二步,设置新的密码

@param     completion-回调代码块

@result    空

*/

- (void) resetPwd2:(void (^)(bool, NSDictionary *))completion;

```

###全局运行数据

```objectivec

/*!

* @method    version

* @descript  获取SDK版本号

* @param     空

* @result    SDK版本号

*/

- (NSString*)version;



/*!

* @method    registerApp

* @descript  通过证书注册应用(必须注册应用才能正常使用sdk)

* @param     certificatePath   证书地址

* @param     cacheFolder       缓存保存地址

* @result    初始化后的缓存地址

*/

- (NSString*)registerApp:(NSString*)certificatePath onCachePath:(NSString*)path;



/*!

* @method    getServeInfo

* @descript  获取指定服务器信息

* @param     serveName 服务器名称或者地址

* @result    服务器信息

*/

- (NSDictionary*)getServeInfo:(NSString*)serveName;



/*!

* @method    chatListModel

* @descript  会话记录

* @param     空

* @result    会话记录列表

*/

-(LDChatListModel *)chatListModel;



/*!

* @method    contactListModel

* @descript  联系人列表

* @param     空

* @result    联系人列表

*/

-(LDContactListModel *)contactListModel;



/*!

* @method    localContact

* @descript  通过id查找本地联系人

* @param     ID-联系人id

* @result    联系人

*/

- (LDContactModel*)localContact:(int64_t)ID;



/*!

* @method    robotListModel

* @descript  机器人列表

* @param     空

* @result    机器人列表

*/

- (LDRobotListModel *)robotListModel;



/*!

* @method    localRobot

* @descript  通过ID获取本地机器人

* @param     ID    机器人id

* @result    机器人

*/

- (LDRobotModel*)localRobot:(int64_t)ID;



/*!

* @method    groupListModel

* @descript  群组列表

* @param     空

* @result    群组列表

*/

- (LDGroupListModel *)groupListModel;



/*!

* @method    localGroup

* @descript  通过ID获取本地群组

* @param     ID    群组id

* @result    群组

*/

- (LDGroupModel*)localGroup:(int64_t)ID;



/*!

* @method    groupMembers

* @descript  当前群的群成员集合

* @param     空

* @result    群成员集合

*/

- (LDGroupMemberListModel*)groupMembers;



/*!

* @method    enterpriseListModel

* @descript  组织架构的企业列表

* @param     空

* @result    企业列表

*/

- (LDEnterpriseListModel *)enterpriseListModel;



/*!

* @method    sysMessage

* @descript  最新系统提示消息

* @param     空

* @result    最新系统提示消息

*/

- (LDSysMsgModel*)sysMessage;



/*!

* @method    mySelfInfo

* @descript  登录用户信息

* @param     空

* @result    登录用户信息

*/

- (LDMyselfModel*)mySelfInfo;



/*!

* @method    loginConfig

* @descript  登录账号信息

* @param     空

* @result    登录账号信息

*/

- (LDAuthModel*)loginConfig;



/*!

* @method    queryEnterpriseList

* @descript  获取组织架构企业列表

* @param     空

* @result    获取组织架构企业列表

*/

- (void)queryEnterpriseList;



/*!

* @method    queryPasswordInfo

* @descript  获取密码强度信息

* @param     空

* @result    获取密码强度信息

*/

- (void)queryPasswordInfo;



/*!

* @method    passwordInfo

* @descript  密码强度信息

* @param     空

* @result    密码强度信息

*/

- (LDPasswordStipulateModel*)passwordInfo;



/*!

* @method    avatar

* @descript  获取头像图片

* @param     avatar    头像名

* @param     image     缺省图片

* @result    头像图片

*/

- (UIImage*)avatar:(NSString*)avatar withDefault:(NSString*)image;



/*!

* @method    imageWithKey

* @descript  获取图片

* @param     key       文件密钥

* @param     imagePath 文件路径

* @param     image     缺省图片

* @result    解密后的图片

*/

- (UIImage*)imageWithKey:(NSString*)key fromPath:(NSString*)imagePath withDefault:(NSString*)image;



/*!

* @method    encryptFile

* @descript  加密文件接口

* @param     srcPath    源文件路径

* @param     targetPath 加密后文件路径

* @param     key        加密秘钥

* @result    加密是否成功

*/

- (bool)encryptFile:(NSString*)srcPath toFile:(NSString*)targetPath withKey:(NSString*)key;



/*!

* @method    idRange

* @descript  id范围(判断id是群、个人、机器人等)

* @param     target    判断对象id

* @result    id范围

*/

-(IDRange)idRange:(int64_t)target;

```

###推送模块

```objectivec

数据同步状态通知 

登录成功后,SDK会立即同步数据(聊天消息、用户资料、用户关系、群资料、离线消息等),并推送给注册监听



/*!

* @method    chatListMoniter

* @descript  监听最近会话列表

* @param     moniter   监听回调

* @result    空

*/

- (void)chatListMoniter:(ChatListMoniter)moniter;



/*!

* @method    contactListMoniter

* @descript  监听联系人列表

* @param     moniter   监听回调

* @result    空

*/

- (void)contactListMoniter:(ContactListMoniter)moniter;



/*!

* @method    messageMoniter

* @descript  新消息监听

* @param     moniter   监听回调

* @result    空

*/

- (void)messageMoniter:(MessageMoniter)moniter forTarget:(int64_t)target;



/*!

* @method    myselfInfoMoniter

* @descript  个人信息变动监听

* @param     moniter   监听回调

* @result    空

*/

- (void)myselfInfoMoniter:(MyselfInfoMoniter)moniter;



/*!

* @method    myselfInfoMoniter

* @descript  个人信息变动监听

* @param     moniter   监听回调

* @result    空

*/

- (void)groupMembersMoniter:(GroupMembersMoniter)moniter;



/*!

* @method    headerRefreshMoniter

* @descript  好友、群、群成员、机器人头像更新并下载到本地后通知

             在需要监听时灵活调用

* @param     moniter   监听回调

* @result    空

*/

- (void)headerRefreshMoniter:(HeaderRefreshMoniter)moniter;



/*!

* @method    kick

* @descript  上下线提醒或者退出或者被踢下线

* @param     moniter   监听回调

* @result    空

*/

- (void)kick:(Kick)moniter;

```

###会话消息

```objectivec

/*!

* @method    isTopChat

* @descript  是否是置顶会话

* @param     空

* @result    是否置顶会话

*/

-(bool)isTopChat;



/*!

* @method    chatOwner

* @descript  用于判断消息来源(个人－区分性别／群)

* @param     空

* @result    消息来源

*/

- (MessageOwner)chatOwner;



/*!

* @method    setMsgReaded

* @descript  设置消息已读

* @param     空

* @result    空

*/

-(void)makeMessageReaded;



/*!

* @method    historyMessages-此方法需要初始化新对象

* @descript  获取本地聊天记录

* @param     block

             回调代码块

* @result    空

*/

- (void)historyMessages:(void (^)(NSError *error,LDMessageListModel *messageList))completion;

/*!

* @method    receivedMessage

* @descript  收到消息时更新对应chat的消息列表

* @param     block

             回调代码块

* @result    空

*/

- (void)receivedMessage:(LDMessageModel*)message;



/*!

* @method    chatMessageList

* @descript  返回会话消息列表

* @param     空

* @result    消息列表

*/

- (LDMessageListModel*)chatMessageList;



/*!

* @method    searchMessagesWithType

* @descript  返回所给类型的本地消息列表

* @param     type 消息类型

* @result    空

*/

-(void)searchMessagesWithType:(MessageType)type completion:(void (^) (NSError* error,LDMessageListModel *messaages))completion;



/*!

* @method    searchMessagesWithKeyword

* @descript  搜索对应关键字并返回对应本地消息列表

* @param     keyword 关键字

* @result    空

*/

-(void)searchMessagesWithKeyword:(NSString *)keyword completion:(void (^) (NSError* error,LDMessageListModel *chatList))completion;



/*!

* @method    sendMessage

* @descript  发送普通文本消息

* @param     message 消息对象

* @param     status 消息发送状态

* @result    空

*/

- (void)sendMessage:(LDMessageModel*)message

           onStatus:(MessageSendStatus)status;



/*!

* @method    sendMessage

* @descript  发送文件消息

* @param     message 消息对象

* @param     progress 文件上传进度

* @param     status 消息发送状态

* @result    空

*/

- (void)sendMessage:(LDMessageModel *)message

         onProgress:(FileUploadProgress)progress

           onStatus:(MessageSendStatus)status;



/*!

* @method    searchListWithKeyword

* @descript  通过关键字搜索chat对象

* @param     completion

* @result    空

*/

-(void)searchChatWithKeyword:(NSString *)keyword

                  completion:(void (^) (NSError* error,NSArray *chats))completion;



/*!

* @method    removeChatRecord

* @descript  删除会话记录

* @param     chatModel

             需要删除的会话

* @param     completion

             删除会话记录回调

* @result    空

*/

- (void)removeChatRecord:(LDChatModel*)chatModel completion:(void (^) (NSError* error))completion;



/*!

* @method    removeHistoryMessageFor

* @descript  删除历史消息

* @param     target

             需要删除历史消息的对象,可以是好友或者群,当target为空是表示删除所有历史消息

* @param     completion

             删除历史消息回调

* @result    空

*/

- (void)removeHistoryMessageFor:(LDItemModel*)target completion:(void (^) (NSError* error))completion;



/*!

* @method    makeTopChat

* @descript  置顶会话

* @param     chatModel

             需要置顶的会话

* @param     completion

             置顶会话回调

* @result    空

*/

- (void)makeTopChat:(LDChatModel*)chatModel completion:(void (^) (NSError* error))completion;



/*!

* @method    roomList

* @descript  获取房间列表

* @param     completion

             获取房间列表回调

* @result    空

*/

- (void)roomList:(void (^) (NSError *error,LDRoomListModel *roomList))completion;

```

###基础消息类型

```objectivec

SDK 提供一套完善的消息传输管理服务，包括收发消息，存储消息，上传下载附件，管理最近联系人等。 

SDK 原生支持发送文本，图片，文件，名片，语音和地理位置等 6 种类型消息，同时支持用户发送自定义的消息类型。



/*!

* @method    loadMedia

* @descript  加载消息文件

* @param     fileData  文件数据data

* @param     progress  加载文件进度

* @result    空

*/

- (void)loadMedia:(FileDownloadResult)fileData onProgress:(FileDownloadProgress)progress;

```

###文本消息

```objectivec

/*!

* @method    initWithText

* @descript  通过字符串初始化文本消息

* @param     text  文本内容

* @result    文本消息

*/

- (instancetype)initWithText:(NSString*)text;

```

###图片消息

```objectivec

/*!

* @method    initWithImage

* @descript  通过图片文件路径初始化图片消息

* @param     imagePath 图片文件路径

* @result    图片消息

*/

- (instancetype)initWithImage:(UIImage*)image;

```

###语音消息

```objectivec

/*!

* @method    initWithAudio

* @descript  通过语音文件路径初始化语音消息

* @param     audioPath 语音文件路径

* @result    语音消息

*/

- (instancetype)initWithAudio:(NSString*)audioPath;

```

###文件消息

```objectivec

/*!

* @method    initWithFile

* @descript  初始化文件消息

* @param     fileurl 语音文件路径

* @result    文件消息

*/

- (instancetype)initWithFile:(NSString *)secretKey

                        sign:(int)fileSign

                     fileURL:(NSString *)fileurl;

```

###名片消息

```objectivec

/*!

* @method    initWithItem

* @descript  初始化名片消息

* @param     item  名片对象(好友、群组等)

* @result    名片消息对象

*/

- (instancetype)initWithItem:(LDItemModel*)item;

```

###位置消息

```objectivec

/*!

* @method    initWithCoordinate

* @descript  初始化位置消息

* @param     coordinate    坐标

* @param     address       坐标对应的地址

* @result    名片消息对象

*/

- (instancetype)initWithCoordinate:(CLLocationCoordinate2D)coordinate andAddress:(NSString*)address;

```

###系统提示消息

```objectivec

/*!

@method    sysMessages

@descript  系统消息列表

@param     block-回调代码块

@result    空

*/

- (void)sysMessages:(void (^) (NSError *error,LDListModel *sysMessageList))completion;



/*!

@method  verifyBuddy

@descript  处理好友请求

@param     处理好友响应代码块

@result    空

*/

-(void)verifyBuddy:(void (^) (NSError *error))completion;



/*!

@method  verifyGroup

@descript  处理入群请求

@param     处理入群请求代码块

@result    空

*/

-(void)verifyGroup:(void (^) (NSError *error))completion;



/*!

@method  sysMsgReaded

@descript  设置系统消息已读

@param     _readType,_readedMsgs 

@result    空

*/

-(void)sysMsgReaded:(void (^) (NSError *error))completion;

```

###好友

```objectivec

/*!

*@method    addStar

*@descript  设置重要好友

*@param     completion 设置重要好友的回调代码块

*@result    空

*/

-(void)addStar:(void (^) (NSError *error))completion;



/*!

*@method    removeStar

*@descript  取消重要好友

*@param     completion 取消重要好友的回调代码块

*@result    空

*/

-(void)removeStar:(void (^) (NSError *error))completion;



/*!

*@method    resetRemark

*@descript  添加备注

*@param     completion 添加好友备注的回调代码块

*@result    空

*/

-(void)resetRemark:(void (^) (NSError *error))completion;



/*!

*@method    modifyChatImage

*@descript  修改聊天背景

*@param     completion 修改聊天背景的回调代码块

*@result    空

*/

-(void)modifyChatImage:(void (^) (NSError *error))completion;



/*!

*@method    searchContacts

*@descript  网络检索

*@param     key     搜索关键字

*@param     area    搜索区域

*@param     type    搜索搜索内容

*@result    返回包含用户,群组,机器人数组的字典

*/

- (void)contactsWithKey:(NSString*)key

                 onArea:(search_area)area

                forType:(search_type)type

             completion:(void (^) (NSError *error,NSDictionary *info))completion;



/*!

*@method    addContact

*@descript  添加好友

*@param     contact 联系人对象 verifyInfo 验证消息（可多条） remark 备注 

*@result    空

*/

-(void)addContact:(LDUserModel *)contact

       verifyInfo:(NSArray<NSString*> *)info

           remark:(NSString *)remark

       completion:(void (^) (NSError *error))completion;



/*!

*@method    removeContact

*@descript  解除好友关系

*@param     contact 联系人对象 delEither 是否同时在对方好友列表里把我删掉 

*@result    空

*/

-(void)removeContact:(LDContactModel*)contact

           delEither:(BOOL)deleteEither

          completion:(void (^) (NSError *error))completion;

```

###群组



####群操作权限 

^权限 ^临时群^ 

|邀请成员 |任何人| 

|可以被搜索 |可以| 

|踢出成员 |群主/管理员| 

|解散群 |群主| 

|退群 |普通群成员/管理员| 

|更改群名称 |群主/管理员| 

|更改群公告 |群主/管理员| 

|更改群介绍 |群主/管理员| 

|转让 |群主|



####群组model提供的接口

```objectivec

/*!

@method    syncGroupInfo

@descript  获取群信息

@param     group_info:获取群详情;group_mem:获取群成员;

@result    空

*/

- (void)syncGroupInfo:(groupInfo)info;



/*!

@method    updateGroupInfo

@descript  修改群资料

@param     空

@result    状态和错误码

*/

- (void)updateGroupInfo:(void (^)(NSError *error))completion;



/*!

@method    modifyGroupIcon

@descript  修改群头像

@param     空

@result    状态和错误码

*/

- (void)modifyGroupIcon:(void (^) (NSError *error))completion;



/*!

@method    modifyChatImage

@descript  修改群聊背景图片

@param     空

@result    状态和错误码

*/

- (void)modifyChatImage:(void (^) (NSError *error))completion;



/*!getGroupVerify

@method    setGroupVerify

@descript  设置加入群的验证方式

@param     空

@result    状态和错误码

*/

- (void)setGroupVerify:(void (^) (NSError *error))completion;



/*!

@method    transferGroup

@descript  转让群

@param     要转让的群成员对象

@result    状态和错误码

*/

- (void)transferGroup:(LDGroupMemberModel *)contact

completion:(void (^) (NSError *error))completion;



/*!

@method    setGroupVsign

@descript  设置群v标

@param     空

@result    状态和错误码

*/

- (void)setGroupVsign:(void (^) (NSError *error))completion;



/*!

@method    changeNotificationType

@descript  设置群消息通知方式

@param     空

@result    状态和错误码

*/

- (void)changeNotificationType:(notification_type)type completion:(void (^) (NSError *error))completion;



/*!

@method    changeNotificationContent

@descript  设置群消息通知内容

@param     空

@result    状态和错误码

*/

- (void)changeNotificationContent:(notification_content)content completion:(void (^) (NSError *error))completion;



/*!

@method    createGroupWithInviteMembers

@descript  创建群聊

@param     需要添加的成员列表

@result    状态和包含新群ID的字典

*/

- (void)createGroupWithInviteMembers:(NSArray <LDUserModel *>*)contactList

                          completion:(void (^)(NSError *error, NSDictionary *info))completion;



/*!

@method    joinGroupWithVerifyInfo

@descript  申请加入群

@param     info 验证信息

@result    状态和错误码

*/

- (void)joinGroup:(LDGroupModel *)group

       VerifyInfo:(NSString *)info

       completion:(void (^)(NSError *error))completion;



/*!

@method    dismissGroup

@descript  解散群

@param     group 群对象

@result    状态和错误码

*/

- (void)dismissGroup:(LDGroupModel *)group

          completion:(void (^)(NSError *error))completion;



/*!

@method    quitGroup

@descript  退出群

@param     group 群对象

@result    状态和错误码

*/

- (void)quitGroup:(LDGroupModel *)group

       completion:(void (^)(NSError *error))completion;

```



####个人信息

```objectivec

/*!

* @method      modifyMyselfHeader

* @descript    用于登录用户修改头像

* @param       block 修改回调

* @result      空

*/

- (void)modifyMyselfHeader:(void (^)(NSError *error, LDMyselfModel *myself))block;



/*!

* @method      modifyMyselfHeader

* @descript    用于登录用户修改个人信息

* @param       block 修改回调

* @result      空

*/

- (void)modifyMyselfBasicInfo:(void (^)(NSError *error, LDMyselfModel *myself))block;



/*!

@method        myselfConfigure

@descript      个人设置项值获取

@param         configure    通过枚举获取指定的值

@result        对应的设置项值

*/

- (NSNumber*)myselfConfigure:(configInfo)configure;



/*!

* @method      modifyMyselfConfigure

* @descript    个人设置相关信息修改

* @param       settingInfo 需要修改的项和对应值

* @result      空

*/

- (void)modifyMyselfConfigure:(NSDictionary *)configureInfo callBack:(void (^) (NSError *error))completion;



/*!

@method    myselfSetting

@descript  个人设置项值获取

@param     info    通过枚举获取指定的值

@result    开启状态

*/

- (BOOL)myselfSetting:(settingInfo)info;



/*!

* @method      modifyUserSetting

* @descript    个人设置信息修改

* @param       settingInfo  需要修改的项

* @result      空

*/

- (void)modifyMyselfSetting:(settingInfo)settingInfo completion:(void (^) (NSError *error))completion;



/*!

@method    noDisturbMode

@descript  全局免打扰状态

@param     空

@result    全局免打扰状态

*/

- (BOOL)noDisturbMode;



/*!

@method    changeNodisturbModel

@descript  改变全局免打扰模式

@param     completion  回调

@result    空

*/

- (void)changeNodisturbModel:(void (^) (NSError *error))completion;



/*!

@method    getCode

@descript  获取验证码

@param     phoneNum    手机好

@result    设置项值

*/

- (void)getCode:(NSString *)phoneNum callBack:(void (^)(NSError *error))completion;



/*!

@method    bindPhone

@descript  绑定手机

@param     info    通过枚举获取指定的值

@result    空

*/

- (void)bindPhone:(NSString *)phone callBack:(void (^)(NSError *error))completion;



/*!

@method    bindEmail

@descript  绑定邮箱

@param     email    邮箱

@result    空

*/

-(void)bindEmail:(NSString *)email callBack:(void (^)(NSError *error))completion;

```



###扩展功能(V1.5.0-高级权限功能)

####黑名单

```objectivec

/*!

*@method    addContactsToBlackList

*@descript  添加好友到黑名单

*@param     contactList 好友数组

*@result    空

*/

- (void)addContactsToBlackList:(NSMutableArray<LDUserModel *> *)contactList

                    completion:(void (^) (NSError *error))completion;



/*!

*@method    removeContactsFromBlackList

*@descript  移除黑名单里的好友

*@param     contactList 好友数组

*@result    空

*/

- (void)removeContactsFromBlackList:(NSMutableArray<LDUserModel *> *)contactList

                         completion:(void (^) (NSError *error))completion;



/*!

*@method    clear

*@descript  清空黑名单

*@param     空

*@result    空

*/

- (void)clear:(void (^) (NSError *error))completion;



/*!

*@method    requestBlackList

*@descript  获取黑名单ID列表

*@param     空

*@result    空

*/

- (void)requestBlackList:(void (^) (NSError *error,NSArray<NSNumber*>* members))completion;

```

####隐藏好友

```objectivec

/*!

*@method    addHiddenID

*@descript  添加隐藏的好友或群组

*@param     items ID数组

*@result    空

*/

-(void)addHiddenID:(NSArray<NSNumber *>*)items

        completion:(void (^) (NSError *error))completion;



/*!

*@method    removeHiddenID

*@descript  删除隐藏的好友或群组

*@param     items ID数组

*@result    空

*/

-(void)removeHiddenID:(NSArray<NSNumber *>*)items

           completion:(void (^) (NSError *error))completion;



/*!

*@method    queryHiddenIDs

*@descript  获取被隐藏的好友

*@param

*@result

*/

-(void)queryHiddenIDs:(void (^) (NSError *error,NSArray *items))completion;



/*!

*@method    resetHiddenPassword

*@descript  修改隐藏好友密码

*@param     

*@result    空

*/

-(void)resetHiddenPassword:(void (^) (NSError *error))completion;

```

####记事本

```objectivec

/*!

*@method    queryNoteByBeginID

*@descript  添加隐藏的好友或群组 起始消息ID offsetFlag = 0 msgBeginID = 0时，代表从最大的消息Id进行查找

*@param     beginID 起始消息ID offset 查询的数量 offsetFlag 0.消息Id由大到小偏移 1.消息Id由小到大偏移 offsetFlag

*@result    completion回调代码块

*/

- (void)queryNoteByBeginID:(long long)beginID

                    offset:(int)offset

                      flag:(int)flag

                completion:(void (^) (NSError *error))completion;



/*!

*@method    addNote

*@descript  添加一个笔记

*@param     note note对象

*@result    completion回调代码块

*/

- (void)addNote:(LDNoteModel *)note

     completion:(void (^) (NSError *error))completion;



/*!

*@method    deleteNotes

*@descript  删除笔记

*@param     IDs 要删除的笔记ID数组

*@result    completion回调代码块

*/

- (void)deleteNotes:(NSArray<NSNumber *>*)IDs

         completion:(void (^) (NSError *error))completion;



/*!

*@method    editNote

*@descript  编辑笔记

*@param     note 修改后的note对象

*@result    completion回调代码块

*/

- (void)editNote:(LDNoteModel *)note

      completion:(void (^) (NSError *error))completion;



/*!

* @method    buildWithTitle

* @descript  创建note对象

* @result    note

*/

+(instancetype)buildWithTitle:(NSString*)title

                      content:(NSString*)content

                      keyword:(NSString *)keyword

                         type:(NoteType)type

                   sourceType:(NoteSource)sourceType;

```

####任务

```objectivec

/*!

* @method    querySendMessages

* @descript  获取发送的任务消息列表

* @result    空

*/

-(void)querySendMessages:(void (^) (NSError *error))completion;



/*!

* @method    queryReceiveMessages

* @descript  获取接受的任务消息列表

* @result    空

*/

-(void)queryReceiveMessages:(void (^) (NSError *error))completion;



/*!

* @method    queryHistoryMessages

* @descript  获取历史任务消息列表

* @result    空

*/

-(void)queryHistoryMessages:(void (^) (NSError *error))completion;



/*!

* @method    sendMessageTo

* @descript  任务发送接口

* @param     target    消息接收方ID

* @param     status    消息发送状态

* @result    空

*/

-(void)sendMessageTo:(int64_t)target onStatus:(MessageSendStatus)status;



/*!

* @method    queryMessageBody

* @descript  查询任务上下文

* @result    空

*/

-(void)queryMessageBody:(void (^) (NSError *error))completion;



/*!

* @method    moveMessageTop

* @descript  任务消息置顶

* @result    空

*/

-(void)moveMessageTop:(void (^) (NSError *error))completion;



/*!

* @method    moveMessageTop

* @descript  恢复任务消息

* @result    空

*/

-(void)recoveryTask:(void (^) (NSError *error))completion;



/*!

* @method    moveMessageTop

* @descript  完成任务消息

* @result    空

*/

-(void)completeTask:(void (^) (NSError *error))completion;

```

####房间

```objectivec

/*!

*@method       createRoom

*@descript     创建房间

*@param        roomName

               房间名称

*@param        chats

               房间包含的会话ID数组

*@result       空

*/

- (void)createRoom:(NSString*)roomName withChats:(NSArray*)chats completion:(void (^) (NSError *error,LDRoomListModel *roomList))completion;



/*!

*@method       removeRoom

*@descript     删除房间

*@param        room

要删除的房间

*@result       空

*/

- (void)removeRoom:(LDRoomModel*)room completion:(void (^) (NSError *error,LDRoomListModel *roomList))completion;



/*!

*@method       updateRoomName

*@descript     修改房间名称

*@param        roomName

房间名称

*@param        completion

房间名称修改结果

*@result       空

*/

- (void)updateRoomName:(NSString*)roomName completion:(void (^) (NSError *error))completion;

```

####多服务器

```objectivec

/*!

* @method    initWithCachePath

* @descript  通过缓存路径初始化子账号

* @param     path   缓存路径

* @result    子账号管理对象

*/

- (instancetype)initWithCachePath:(NSString*)path;



/*!

* @method    loginWithAccount-子账号手动登录,用于添加子账号

* @descript  全局登录接口

* @param     account    登录帐号

* @param     password   登录密码

* @param     loginType  登录类型

* @param     region 国家或者地区编码

* @param     domain 服务器标识或者服务器地址

* @param     completion 登录结果(error为空表示成功,失败有具体失败原因说明)

* @result    空

*/

- (void)loginWithAccount:(NSString*)account

                password:(NSString*)pwd

               loginType:(login_type)loginType

                  region:(NSString*)regionCode

                  domain:(NSString *)domain

              completion:(void (^) (NSError *error))completion;



/*!

* @method    loginWithLoginAuth-子账号自动登录

* @descript  全局登录接口

* @param     loginAuth  主账号关联的子账号信息

* @result    空

*/

- (void)loginWithLoginAuth:(LDAuthModel*)loginAuth

                completion:(void (^) (NSError *error))completion;



/*!

*@method       loadOfflineMessage

*@descript     同步消息

*@param        空

*@result       空

*/

- (void)loadOfflineMessage;



/*!

*@method       numberOfUnreadMessage

*@descript     未读消息数

*@param        空

*@result       空

*/

- (NSInteger)numberOfUnreadMessage;



/*!

* @method    multiServerInfo

* @descript  获取子账号列表

* @param     空

* @result    子账号列表

*/

- (NSArray*)multiServerInfo;



/*!

* @method    bindMultiServer

* @descript  绑定子账号

* @param     servers    子账号列表

* @result    空

*/

- (bool)bindMultiServer:(NSArray<LDMultiServerModel *>*)servers;



/*!

* @method    switchMultiServer

* @descript  切换主帐号

* @param     server 需要切换为主账号的账号

* @result    空

*/

- (bool)switchMultiServer:(LDMultiServerModel*)server;

```
