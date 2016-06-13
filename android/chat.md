##聊天 
`ChatMsgService chatMsgService = SDKClient.instance().getChatMsgService()`
###发送消息
 传入参数：（消息对象，ResultCallBack）
返回发送的ChatMsg,根据chatMsg.getMsgStatus展示 消息发送成功，发送失败，发送中状态
```
chatMsgService.sendMsg(ChatMsg chatMsg, ResultCallBack<ChatMsg> callBack); 
```
###构造不同消息对象
(ChatMsgBuilder 提供构造部分具体ChatMsg对象)
```
ChatMsgBuilder builder = new ChatMsgBuilder(targetID);
builder.createTxtMsg("").setRelatedUsers(ArrayList<Long>);
ChatMsg chatMsg = builder.build();
```
###接收消息
聊天界面收到当前会话消息通过监听返回
```
chatMsgService.setReceiveListener(long targetID, OnReceiveChatMsgListener listener);
```
###接收消息通知（全局接收）
```
SDKClient.instance().getChatService().setNotificationListener(OnNotificationListener listener);
```
###拉取历史记录
传入参数：（聊天对象ID，	起始消息ID，偏移，ResultCallBack）
callBack返回结果为按时间排序的chatMsg列表
```
chatMsgService.getHistoryMsg(long targetID, long beginID, int offset, ResultCallBack<ArrayList<ChatMsg>> callBack);
```
###设置消息为已读 
传入参数（聊天对象ID，最后一条未读消息ID），不用传入回调
```
chatMsgService.setMsgRead(long targetID, long messageID) ;
```
###本地消息全局搜索
返回：每个匹配到的群或个人的消息的数目
```
    /**
     * @param targetID
     * 　targetId为用户Id或群Id，与count字段共同决定搜索的方式，有以下几种组合：
     *   targetId !=0, count = 1:搜索指定的targetId的聊天记录数目。
     * 　targetId = 0,count > 1: 从最小的targetId开始向上搜索记录，共搜索到count个匹配的targetId为止。
     *   targetId !=0, count >1: 从指定的targetId开始向上搜索记录，共搜索到count个匹配的targetId为止。
     *   count = 0为匹配全部消息，最多匹配10000条
     * @param count     //一次匹配到最大的消息数量,0为匹配全部消息,最多匹配100000条
     * @param msgType   ///搜索消息的类型，1:html 2:文本，3:音频 4: 位置 5:图片6:文件 7:名片 8:弱提示 (当前只支持文本)
     * @param key       //搜索的关键字
     * @param startTime //搜索消息的最小时间,不能大于endTime,单位秒
     * @param endTime   //搜索消息的最大时间,0为搜索全部时间段,单位秒
     * @param callBack
     * @return
     */
    chatMsgService.msgGlobalSearch(long targetID, int count, short msgType, String key, long startTime, long endTime, ResultCallBack<MsgGlobalSearchResult> callBack)
```
###个人或者群的聊天记录中搜索关键字
```
    /**
     * 在某个群或个人的聊天记录中搜索关键字
     *
     * @param targetID
     * @param count     //一次匹配到最大的消息数量,0为匹配全部消息,最多匹配100000条
     * @param msgType   ///搜索消息的类型，1:html 2:文本，3:音频 4: 位置 5:图片6:文件 7:名片 8:弱提示 (当前只支持文本)
     * @param msgID     起始msgId，0为从最早的消息就行搜索
     * @param key       //搜索的关键字
     * @param startTime //搜索消息的最小时间,不能大于endTime,单位秒
     * @param endTime   //搜索消息的最大时间,0为搜索全部时间段,单位秒
     * @param callBack
     * @return
     */
chatMsgService.msgDetailSearch(long targetID, int count, int msgType,int msgID, String key, long startTime, long endTime, ResultCallBack<MsgDetailSearchResult> callBack)
```
###外部文件下载命令
```
      /**
     * @param localPath  文件本地保存路径 localPath.
     * @param remotePath 远程路径完整的URL路径 remotePath.
     * @param callBack
     * @return
     */
    chatMsgService.downloadFile(String localPath, String remotePath, ResultCallBack callBack) 
```
###得到保存文件路径
```
chatMsgService.getFileInfos(ArrayList<Long> fileMsgIds, ResultCallBack<FileInfoResult> callBack)
```
###根据消息类型获取消息列表
```
chatMsgService.getMsgsByType(long targetID, int msgType, ResultCallBack<ArrayList<ChatMsg>> callBack)
```
###获取网址缩略图信息
```
chatMsgService.getUrlInfo(String url, ResultCallBack<ArrayList<ChatMsg>> callBack)
```
###删除消息
传入参数：（聊天对象ID，删除消息ID列表）
```
chatMsgService.deleteByID(long targetID, ArrayList<Long> msgIDs) ;
```
传入参数：（聊天对象ID，起始时间，结束时间）当时间都为0时删除所有消息
```
chatMsgService.deleteByTime(long targetID, long startTime, long endTime) ;
```
删除此聊天记录中所有消息
```
chatMsgService.deleteAll(long targetID)
```
####转发消息
```
chatMsgService.transferMsg(long targetID,ChatMsg chatMsg, ResultCallBack<Long> callBack)
```
####置顶任务
```
chatMsgService.topTask(long msgID,ResultCallBack callBack)
```
####任务列表
返回 ArrayList<TaskMsgBean>
```
chatMsgService.getHistoryTasks(ResultCallBack<ArrayList<TaskMsgBean>> callBack)
```
####获取指派任务列表
```
chatMsgService.getSendTasks(ResultCallBack<ArrayList<TaskMsgBean>> callBack)
```
####获取接收到的任务列表
```
chatMsgService.getReceiveTasks(ResultCallBack<ArrayList<TaskMsgBean>> callBack)
```
####获取任务消息体
```
chatMsgService.getTaskBody(long msgID,ResultCallBack<String> callBack)
```
####恢复任务
```
chatMsgService.recoveryTask(long msgID,ResultCallBack callBack)
```
####完成任务
```
chatMsgService.finishTasK(long msgID,ResultCallBack callBack)
```
###记事本
####添加记事本
```
chatMsgService.addNote(NoteInfoBean bean, ResultCallBack callBack)
```
####获取记事本
```
    /**
     * @param beginID    起始消息ID offsetFlag = 0 msgBeginID = 0时，代表从最大的消息Id进行查找
     * @param offSet     查询的数量
     * @param offSetFlag 偏移标志；0.消息Id由大到小偏移 1.消息Id由小到大偏移.
     * @param callBack
     * @return
     */
chatMsgService.getAllNotes(long beginID, int offSet, byte offSetFlag, ResultCallBack<ArrayList<NoteInfoBean>> callBack)
```
####删除记事本
```
chatMsgService.deleteNotes(ArrayList<Long> list, ResultCallBack callBack)
```
####修改记事本
```
    /**
     * @param bean     附件记事本只能修改标题，关键字（标签）,文本类可以修改内容
     * @param callBack
     * @return
     */
chatMsgService.editNote(NoteInfoBean bean, ResultCallBack callBack) 
```

##会话列表 
`ChatService chatService = SDKClient.instance().getChatService()`
###获取会话列表
返回按时间排序的会话列表 
```
List<Chat> list = chatService.getList();
```
###未读总数 
```
int unRead = chatService.getTotalUnread();
```
###删除会话
传入参数：(会话ID，ResultCallBack)
删除数据通过消息监听更新数据，不需要主动调用删除列表

```
chatService.delete(long id, ResultCallBack callBack)
```
###置顶会话
传入参数：(会话ID，是否置顶,ResultCallBack)
置顶数据通过消息监听更新数据，不需要主动调用设置对象属性

```
chatService.top(long id,boolean top, ResultCallBack callBack)
```
###清除所有聊天记录
```
chatService.clearAll( ResultCallBack callBack)
```
###设置消息监听（增删改)
对于会话列表，通讯录，群，群成员的增删改都是通过对应的对象设置setListener(OnChangeListener listener)监听更新数据

```
chatService.setListener(OnChangeListener listener);
```
###创建房间
传入参数：（房间名称，最近联系人IDs, ResultCallBack<ChatRoomBean>）
返回：创建成功后返回房间对象ChatRoomBean

```
chatService.createRoom(String name,ArrayList<Long> members,ResultCallBack<ChatRoomBean> callBack)
```
###重命名房间
传入参数：（房间ID，重命名，ResultCallBack）

```
chatService.reNameRoom(long roomID,String name,ResultCallBack callBack)
```
###删除房间
传入参数：（房间ID，ResultCallBack）

```
chatService.deleteRoom(long roomID,ResultCallBack callBack)
```
###获取所有房间
返回：所有房间列表

```
chatService.getAllRooms(ResultCallBack<ArrayList<ChatRoomBean> callBack>)
```
###查询房间
传入参数：（房间ID，ResultCallBack<ChatRoomBean>）
返回：ChatRoomBean

```
chatService.getRoomByID(long roomID, ResultCallBack<ChatRoomBean> callBack)
```

##通讯录 
`ContactService contactService = SDKClient.instance().getContactService()`
###同步调用返回通讯录列表
```
ArrayList<Contact> contactList = contactService.getList();
```
###添加更新删除监听调用
```
contactService.setListener(OnChangeListener listener);
```
###添加好友
 - 获取好友验证方式 
 传入参数：（好友ID，ResultCallBack<Byte>)
 返回好友验证方式，具体参考Constants.TYPE_NOT_ALLOW,Constants.TYPE_VERIFY,Constants.TYPE_EVERY
 
```
contactService.getVerifyType(long userID, ResultCallBack<Byte> callBack);
```
- 添加好友
传入参数：（好友ID，验证信息，备注 ，ResultCallBack）

```
contactService.addContact(long userID, String verifyInfo, String remark, ResultCallBack callBack);
```
### 删除好友
传入参数：（好友ID，ResultCallBack）

```
contactService.removeContact(long userID, ResultCallBack callBack);
```
###获取黑名单列表
传入参数：（ResultCallBack）回掉返回黑名单ID列表

```
contactService.getBlackList(ResultCallBack<ArrayList<Long>> callBack);
```
###添加黑名单
传入参数 ：（黑名单列表，ResultCallBack）

```
contactService.addBlack(ArrayList<Long> blacks, ResultCallBack callBack);
```
###移除黑名单
传入参数 ：（移除列表，ResultCallBack）
**注：当移除列表为空时表示移除所有黑名单**

```
contactService.removeBlack(ArrayList<Long> blacks, ResultCallBack callBack);
```
###隐藏好友
传入参数：（隐藏密码，隐藏好友ID列表，ResultCallBack）

```
contactService.hiddenContact(String password,ArrayList<Long> list,ResultCallBack callBack);
```
###删除隐藏好友
传入参数：（隐藏密码，删除好友ID列表，ResultCallBack）

```
contactService.removeHiddenContact(String password,ArrayList<Long> list,ResultCallBack callBack);
```
###获取隐藏好友
```
contactService.getHiddenContact(String password, ResultCallBack<ArrayList<Long>> callBack)
```
**说明：以下接口都是在被修改的通讯录对象contact上操作**
### 修改备注
```
contact.modifyRemark(String remark,ResultCallBack callBack)
```
###设置V标
```
contact.addStar(ResultCallBack callBack)
```
###取消V标
```
contact.removeStar(ResultCallBack callBack)
```
###设置好友聊天背景
```
contact.setChatImage(String imagePath , ResultCallBack callBack);
```
###本地搜索
传入参数 ：（搜索关键字，callBack）回调返回List<ItemModel>
```
contactService.searchLocal(String key, ResultCallBack<List<ItemModel>> callBack);
```
###网络搜索
传入参数 ：（搜索关键字，callBack）回调返回List<ItemModel>

```
contactService.searchNet(String key, ResultCallBack<List<ItemModel>> callBack) 
```
###获取好友在线状态
```
/**
* @param buddyIds 好友列表 , 如果列表为空，
*                 表示获取全部好友状态，否则获取指定成员状态。
* @param callBack
 * @return
*/
contactService.getOnline(ArrayList<Long> buddyIds, ResultCallBack<OnlineResult> callBack) 
```
###面对面加好友
* (返回结果说明 result：1：加入或者创建成功，2：创建失败，精度、纬度、房间密码不符合要求 3：已与房主是好友关系, 4:房间不存在)
####创建面对面加好友的房间
* 返回：code:　0:成功，100:参数错误，11100:内部错误 FaceToFaceJoinResult 含有randomCode,即服务器产生的password
```
contactService.faceToFaceCreateRoom(long userID, double latitude, double longitude, ResultCallBack<FaceToFaceJoinResult> callBack)
```
####加入面对面加好友的房间
* 返回：code:　0:成功，100:参数错误，11100:内部错误 
```
contactService.faceToFaceJoinRoom(long userID, double latitude, double longitude, String password, ResultCallBack<FaceToFaceJoinResult> callBack)
```
####添加面对面房间中的好友
* 返回：code: 0:成功，100:参数错误，340:没有权限操作（非管理员）， 556:操作失败，345:房间不存在，11100:内部错误
```
contactService.faceToFaceAddBuddy(long userId, String roomId, String verifyInfo,  ArrayList<Long> userList, ResultCallBack callBack)
```
####退出面对面加好友的房间
* 返回：code:　0:成功，100:参数错误，11100:内部错误
```
contactService.faceToFaceExit(long userId, String roomId, ResultCallBack callBack)
```
####设置面对面加好友推送监听
```
contactService.setFaceToFaceListener(OnFaceToFaceListener listener);
```

##群 
`GroupService grouService = SDKClient.instance().getGroupService()`
###获取群列表
```
ArrayList<Group> groupList = groupService.getGroups();
```
###创建群
```
groupService.createGroupByID(ArrayList<Long> inviteIDs, ResultCallBack callBack);
```
###获取群验证方式
```
groupService.getVerifyType(long groupID, ResultCallBack<Byte> callBack);
```
###添加群
```
groupService.addGroup(long groupID, String verifyInfo, ResultCallBack callBack);
```
###获取群详情
传入参数：（群ID，ResultCallBack）
```
groupService.getInfo(long groupID, ResultCallBack<Group> callBack);
```
###面对面建群
* (返回结果说明 result：1：加入或者创建成功，2：创建失败，精度、纬度、房间密码不符合要求 3：已与房主是好友关系, 4:房间不存在)

####创建面对面建群的房间
* 返回：code:　0:成功，100:参数错误，11100:内部错误 FaceToFaceJoinResult 含有randomCode,即服务器产生的password
```
groupService.faceToFaceCreateRoom(long groupId, double latitude, double longitude, ResultCallBack<FaceToFaceJoinResult> callBack)
```

####加入面对面建群的房间
* 返回：code:　0:成功，100:参数错误，11100:内部错误 
```
groupService.faceToFaceJoinRoom(long userID, double latitude, double longitude, String password, ResultCallBack<FaceToFaceJoinResult> callBack)
```

####邀请面对面房间中的好友加入群（groupLevel 1： 临时群  2：普通群）
* 返回：code: 0:成功，100:参数错误，302:没有权限创建群（非管理员） 344:创建群失败，345:房间不存在，11100:内部错误
```
groupService.faceToFaceCreateGroup(long userId, String roomId, byte groupLevel, ArrayList<Long> userList, ResultCallBack callBack)
```

####退出面对面建群的房间
* 返回：code:　0:成功，100:参数错误，11100:内部错误
```
groupService.faceToFaceExit(long userId, String roomId, ResultCallBack callBack)
```

###面对面加群推送监听
```
groupService.setFaceToFaceListener(ContactService.OnFaceToFaceListener listener);
```
**说明：以下接口都是在群对象group上操作**
###获取群成员列表
传入参数：（ResultCallBack）回调返回成员列表
```
group.getMemberList(ResultCallBack<ArrayList<Contact>> callBack);
```
###获取群成员详细信息
```
group.getMemberInfo(long memberID, ResultCallBack<GroupMember> callBack)
``` 
###设置群成员信息
```
group.setMemberInfo(GroupMember groupMember, ResultCallBack callBack);
```
###设置群默认聊天背景
```
group.setChatImageByAdmin(String  chatImage,ResultCallBack callBack)
```
###修改群头像
```
group.modifyAvatar(String avatar, ResultCallBack callBack);
```
###修改群信息
```
group.modifyGroupInfo(Group groupInfo, ResultCallBack callBack);
```
###获取群文件列表
```
group.getFileList(long msgBeginID,int offSet,boolean upSet,ResultCallBack<GroupFilesResult> callBack)
```
###设置群提醒方式
传入参数：（消息提醒方式，接收时间段 ，ResultCallBack）
```
group.setMsgReminderType(byte msgSetType,String receiveTime,ResultCallBack callBack)
```
###获取群消息提醒方式
```
group.getMsgReminderType(ResultCallBack<GroupMessageShieldResult> callBack)
```
####设置群验证方式
传入参数：（验证方式，允许加入，ResultCallBack）
```
group.setVerifyType(byte verifyType,byte isAllow,ResultCallBack callBack)
```
###删除/解散/退出群
```
/**删除/退出群*/
group.exit(ResultCallBack callBack);
//转让群
group.transfertransfer(Contact contact, ResultCallBack callBack);
```
###邀请群成员
```
group.addMemberListByID(ArrayList<Long> inviteIDs, ResultCallBack callBack);
```
###删除群成员
```
group.removeMember(Contact contact, ResultCallBack callBack);
```


