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

##企业组织 
`EnterpriseService enterpriseService = SDKClient.instance().getEnterpriseService()`
###获取企业
```
enterpriseService.getEntList(ResultCallBack<ArrayList<EnerpriseBean>> callBack);
```
###获取组织成员列表
传入参数：（企业id，组织id ，callBak）
企业根组织第一次获取传（0，0）
组织ID在第一次取得时候传0，之后传入要获取的组织ID
返回结果：回调中返回组织和成员列表

```
enterpriseService.getOrgAndUserList(long enterpriseID,long organizeID,ResultCallBack<OrgAndUserListResult> callBack)
```