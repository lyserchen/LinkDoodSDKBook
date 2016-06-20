##聊天 
```java
ChatMsgService chatMsgService = SDKClient.instance().getChatMsgService()
```
###发送消息
 传入参数：（消息对象，ResultCallBack）
返回发送的ChatMsg,根据chatMsg.getMsgStatus展示 消息发送成功，发送失败，发送中状态
```java
chatMsgService.sendMsg(ChatMsg chatMsg, ResultCallBack<ChatMsg> callBack); 
```
###构造不同消息对象
(ChatMsgBuilder 提供构造部分具体ChatMsg对象)
```java
ChatMsgBuilder builder = new ChatMsgBuilder(targetID);
builder.createTxtMsg("").setRelatedUsers(ArrayList<Long>);
ChatMsg chatMsg = builder.build();
```
###接收消息
聊天界面收到当前会话消息通过监听返回
```java
chatMsgService.setReceiveListener(long targetID, OnReceiveChatMsgListener listener);
```
###接收消息通知（全局接收）
```java
SDKClient.instance().getChatService().setNotificationListener(OnNotificationListener listener);
```
###拉取历史记录
传入参数：（聊天对象ID，	起始消息ID，偏移，ResultCallBack）
callBack返回结果为按时间排序的chatMsg列表
```java
chatMsgService.getHistoryMsg(long targetID, long beginID, int offset, ResultCallBack<ArrayList<ChatMsg>> callBack);
```
###设置消息为已读 
传入参数（聊天对象ID，最后一条未读消息ID），不用传入回调
```java
chatMsgService.setMsgRead(long targetID, long messageID) ;
```
###本地消息全局搜索
返回：每个匹配到的群或个人的消息的数目
```java
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
```java
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
```java
      /**
     * @param localPath  文件本地保存路径 localPath.
     * @param remotePath 远程路径完整的URL路径 remotePath.
     * @param callBack
     * @return
     */
    chatMsgService.downloadFile(String localPath, String remotePath, ResultCallBack callBack) 
```
###得到保存文件路径
```java
chatMsgService.getFileInfos(ArrayList<Long> fileMsgIds, ResultCallBack<FileInfoResult> callBack)
```
###根据消息类型获取消息列表
```java
chatMsgService.getMsgsByType(long targetID, int msgType, ResultCallBack<ArrayList<ChatMsg>> callBack)
```
###获取网址缩略图信息
```java
chatMsgService.getUrlInfo(String url, ResultCallBack<ArrayList<ChatMsg>> callBack)
```
###删除消息
传入参数：（聊天对象ID，删除消息ID列表）
```java
chatMsgService.deleteByID(long targetID, ArrayList<Long> msgIDs) ;
```
传入参数：（聊天对象ID，起始时间，结束时间）当时间都为0时删除所有消息
```java
chatMsgService.deleteByTime(long targetID, long startTime, long endTime) ;
```
删除此聊天记录中所有消息
```java
chatMsgService.deleteAll(long targetID)
```
####转发消息
```java
chatMsgService.transferMsg(long targetID,ChatMsg chatMsg, ResultCallBack<Long> callBack)
```
####置顶任务
```java
chatMsgService.topTask(long msgID,ResultCallBack callBack)
```
####任务列表
返回 ArrayList<TaskMsgBean>
```java
chatMsgService.getHistoryTasks(ResultCallBack<ArrayList<TaskMsgBean>> callBack)
```
####获取指派任务列表
```java
chatMsgService.getSendTasks(ResultCallBack<ArrayList<TaskMsgBean>> callBack)
```
####获取接收到的任务列表
```java
chatMsgService.getReceiveTasks(ResultCallBack<ArrayList<TaskMsgBean>> callBack)
```
####获取任务消息体
```java
chatMsgService.getTaskBody(long msgID,ResultCallBack<String> callBack)
```
####恢复任务
```java
chatMsgService.recoveryTask(long msgID,ResultCallBack callBack)
```
####完成任务
```java
chatMsgService.finishTasK(long msgID,ResultCallBack callBack)
```
###记事本
####添加记事本
```java
chatMsgService.addNote(NoteInfoBean bean, ResultCallBack callBack)
```
####获取记事本
```java
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
```java
chatMsgService.deleteNotes(ArrayList<Long> list, ResultCallBack callBack)
```
####修改记事本
```java
    /**
     * @param bean     附件记事本只能修改标题，关键字（标签）,文本类可以修改内容
     * @param callBack
     * @return
     */
chatMsgService.editNote(NoteInfoBean bean, ResultCallBack callBack) 
```

##会话列表 
```java
ChatService chatService = SDKClient.instance().getChatService()
```
###获取会话列表
返回按时间排序的会话列表 
```java
List<Chat> list = chatService.getList();
```
###未读总数 
```java
int unRead = chatService.getTotalUnread();
```
###删除会话
传入参数：(会话ID，ResultCallBack)
删除数据通过消息监听更新数据，不需要主动调用删除列表

```java
chatService.delete(long id, ResultCallBack callBack)
```
###置顶会话
传入参数：(会话ID，是否置顶,ResultCallBack)
置顶数据通过消息监听更新数据，不需要主动调用设置对象属性

```java
chatService.top(long id,boolean top, ResultCallBack callBack)
```
###清除所有聊天记录
```java
chatService.clearAll( ResultCallBack callBack)
```
###设置消息监听（增删改)
对于会话列表，通讯录，群，群成员的增删改都是通过对应的对象设置setListener(OnChangeListener listener)监听更新数据

```java
chatService.setListener(OnChangeListener listener);
```
###创建房间
传入参数：（房间名称，最近联系人IDs, ResultCallBack<ChatRoomBean>）
返回：创建成功后返回房间对象ChatRoomBean

```java
chatService.createRoom(String name,ArrayList<Long> members,ResultCallBack<ChatRoomBean> callBack)
```
###重命名房间
传入参数：（房间ID，重命名，ResultCallBack）

```java
chatService.reNameRoom(long roomID,String name,ResultCallBack callBack)
```
###删除房间
传入参数：（房间ID，ResultCallBack）

```java
chatService.deleteRoom(long roomID,ResultCallBack callBack)
```
###获取所有房间
返回：所有房间列表

```java
chatService.getAllRooms(ResultCallBack<ArrayList<ChatRoomBean> callBack>)
```
###查询房间
传入参数：（房间ID，ResultCallBack<ChatRoomBean>）
返回：ChatRoomBean

```java
chatService.getRoomByID(long roomID, ResultCallBack<ChatRoomBean> callBack)
```

## 系统消息 
```java
SystemMsgService sysMsgService = SDKClient.instance().getSysMsgService()
```
###获取系统消息列表
传入参数：（时间，偏移量，ResultCallBack)
回调中返回系统消息列表

```java
sysMsgService.getList(long time, int offSet, ResultCallBack<ArrayList<SystemMsg>> callBack);
```
###设置系统消息已读
传入参数：（需要设置系统消息列表）

```java
sysMsgService.setRead(ArrayList<SystemMsg> list);
```
###同意好友请求
传入参数：（系统消息ID，好友ID，备注，ResultCallBack）

```java
sysMsgService.agreeContact(long msgID, long userID, String remark, ResultCallBack callBack);
```
###拒绝好友请求
传入参数：（系统消息ID，好友ID，拒绝理由，ResultCallBack）

```java
sysMsgService.refuseContact(long msgID, long userID, String reason, ResultCallBack callBack);
```
