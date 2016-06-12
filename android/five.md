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