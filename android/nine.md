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