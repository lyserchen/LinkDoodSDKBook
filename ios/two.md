## SDK主要提供的类与方法
###全局信息
LDClicent 管理全局运行数据,包括最近会话列表、联系人列表、群组列表以及登录用户信息的管理.

###通知模块
LDNotify 监听所有数据更新,包括最近会话列表、联系人列表、群组列表以及登录用户信息的更新,用于通知应用刷新界面.

###认证模块
LDAuthModel 认证模块，完成认证相关的基本操作

LDRegisterModel 用于注册和找回密码

LDPasswordStipulateModel 获取当前配置的密码强度

###消息模块
LDChatListModel 最近会话列表

LDChatModel 最近会话

LDMessageListModel 会话消息列表

LDMessageModel 消息结构体基类

LDTextMessageModel  文本消息

LDImageMessageModel 图片消息

LDAudioMessageModel 语音消息

LDFileMesssageModel 文件消息

LDCardMesssageModel 名片消息

LDLocationMesssageModel 位置消息

LDSysMsgListModel 系统消息模块，提供系统消息的基本操作，如系统消息获取、删除等

LDSysMsgModel 系统消息信息内容

###联系人模块
LDUserModel 所有聊天对象的信息基类

LDContactModel 好友信息

LDContactListModel 联系人列表

LDMyselfModel 登录用户信息

LDGroupModel 群信息

LDGroupListModel 群列表

LDGroupMemberModel 群成员信息内容

LDGroupMemberListModel 群成员列表相关操作

LDGroupFileModel 群文件信息

###组织架构模块(V1.5.0-高级权限功能)
LDEnterpriseListModel 企业列表

LDEnterpriseUserSearch 组织成员

LDEntpriseModel 企业

LDEntpriseUserModel 组织成员

LDOrganizationContentsListModel 组织和组织成员列表

LDOrganizationModel 组织

###扩展功能(V1.5.0-高级权限功能)
LDBlackContactsModel 黑名单

LDFaceToFaceModel 面对面加好友

LDPrivacyModel 隐藏好友

LDNoteListModel 记事本列表

LDNoteModel 记事本信息

LDTaskMessageListModel 任务列表

LDTaskMessageModel 任务信息

LDRoomListModel 房间列表

LDRoomModel 房间信息

LDMultiServerModel 多服务器子账号信息
