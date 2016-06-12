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