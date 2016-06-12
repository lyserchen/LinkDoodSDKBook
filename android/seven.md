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