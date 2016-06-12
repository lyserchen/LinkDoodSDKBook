## 系统消息 
`SystemMsgService sysMsgService = SDKClient.instance().getSysMsgService()`
###获取系统消息列表
传入参数：（时间，偏移量，ResultCallBack)
回调中返回系统消息列表
```
sysMsgService.getList(long time, int offSet, ResultCallBack<ArrayList<SystemMsg>> callBack);
```
###设置系统消息已读
传入参数：（需要设置系统消息列表）
```
sysMsgService.setRead(ArrayList<SystemMsg> list);
```
###同意好友请求
传入参数：（系统消息ID，好友ID，备注，ResultCallBack）
```
sysMsgService.agreeContact(long msgID, long userID, String remark, ResultCallBack callBack);
```
###拒绝好友请求
传入参数：（系统消息ID，好友ID，拒绝理由，ResultCallBack）
```
sysMsgService.refuseContact(long msgID, long userID, String reason, ResultCallBack callBack);
```
