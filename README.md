## 我的保险接口 ###
### 1.投保列表查询 ####
#### 基本信息
    请求类型：HTTP
    请求地址：http://127.0.0.1:8080/policy/listApplyPolicys
    请求方式：get
    请求类型：String ，int ,int,String
    响应类型：R
#### 接口描述
    本接口是查询企业的投保信息
    1.如果userId为null或者“”，抛出异常
    2.如果没有数据，返回无数据
#### 请求数据
 <table>
       <tr>
           <th>参数名称</th>
           <th>是否必填</th>
           <th>描述</th>
           <th>默认值</th>
       </tr>  
       <tr>
           <td>userId</td>
           <td>√</td>
           <td>查询用户id</td>
           <td></td>
       </tr>  
       <tr>
          <td>pageNum</td>
          <td>√</td>
          <td>第几页</td>
          <td></td>
       </tr>  
       <tr>
         <td>pageSize</td>
         <td>√</td>
         <td>每页记录数</td>
         <td></td>
       </tr>
       <tr>
           <td>token</td>
           <td>√</td>
           <td>登录验证</td>
           <td></td>
       </tr>
   </table>
#### 响应数据
   <table>
      <tr>
          <th>参数名称</th>
          <th>是否必填</th>
          <th>描述</th>
          <th>默认值</th>
      </tr>  
      <tr>
          <td>page</td>
          <td>√</td>
          <td>分页对象</td>
          <td></td>
      </tr>   
  </table>
#### 实例
 请求参数：  
 {
    "userId":"zhangsan",
    "token":"154dfsdff48313s1ve844313131fsd8"
 }  
  响应参数：  
```json
{
  "code":200,  
   "msg":"success",  
   "page":  
{  
   "total":0,  
    "pages":0,  
    "size":1,  
    "pageSize":0,  
   "list":[  
             {  
               "amount":50000,  
               "rate":0.02,  
               "input_time":{  
                    "date":5,  
                    "hours":14,  
                    "seconds":29,  
                    "month":0,  
                    "timezoneOffset":-480,  
                    "year":118,  
                    "minutes":15,  
                    "time":1515132929635,  
                    "day":5  
                  },  
               "business_no":"1236478999",  
               "risk_code":"123",  
               "status":"1"  
             }  
           ],   
       "pageNum":0  
}
}  
```
#### 数据库操作
  根据userId查询投保列表  
```sql
  select gu.business_no,gu.risk_code,gp.product_name risk_name,gu.amount,gu.rate,gu.input_time,gu.status   
     from gupolicymain gu left join ggproduct gp on gu.risk_code= gp.product_id  where gu.insure_appli = #{userId} and gu.status <> '5' order by gu.update_time desc
```
---
### 2.分页查询
#### 基本信息
     请求类型：HTTP
     请求地址：http://127.0.0.1:8080/policy/listApplyPolicysContinue
     请求方式：get
     请求类型：String ， int，int ,String
     响应类型：R
#### 接口描述
     本接口是查询企业的投保信息
     1.如果userId为null或者“”，抛出异常
     2.如果没有数据，返回无数据
#### 请求数据
   <table>
        <tr>
            <th>参数名称</th>
            <th>是否必填</th>
            <th>描述</th>
            <th>默认值</th>
        </tr>  
        <tr>
            <td>userId</td>
            <td>√</td>
            <td>查询用户id</td>
            <td></td>
        </tr>   
        <tr>
          <td>pageNum</td>
          <td>√</td>
          <td>第几页</td>
          <td></td>
       </tr>  
       <tr>
         <td>pageSize</td>
         <td>√</td>
         <td>每页记录数</td>
         <td></td>
       </tr>   
        <tr>
            <td>token</td>
            <td>√</td>
            <td>登录验证</td>
            <td></td>
        </tr>
    </table>
#### 响应数据
   <table>
       <tr>
           <th>参数名称</th>
           <th>是否必填</th>
           <th>描述</th>
           <th>默认值</th>
       </tr>  
       <tr>
           <td>page</td>
           <td>√</td>
           <td>分页对象</td>
           <td></td>
       </tr>   
   </table> 
#### 实例
  请求参数：  
  {
     "userId":"zhangsan",
     "token":"154dfsdff48313s1ve844313131fsd8"
  }  
   响应参数： 
```json 
{
  "code":200,  
   "msg":"success",  
   "page":  
  {  
     "total":0,  
      "pages":0,  
      "size":1,  
      "pageSize":0,  
     "list":[  
               {  
                 "amount":50000,  
                 "rate":0.02,  
                 "input_time":{  
                      "date":5,  
                      "hours":14,  
                      "seconds":29,  
                      "month":0,  
                      "timezoneOffset":-480,  
                      "year":118,  
                      "minutes":15,  
                      "time":1515132929635,  
                      "day":5  
                    },  
                 "business_no":"1236478999",  
                 "risk_code":"123",  
                 "status":"1"  
               }  
             ],   
         "pageNum":0  
  }
}  
```
#### 数据库操作
   根据userId查询投保列表  
```sql
   select gu.business_no,gu.risk_code,gp.product_name risk_name,gu.amount,gu.rate,gu.input_time,gu.status   
   from gupolicymain gu left join ggproduct gp on gu.risk_code= gp.product_id  where gu.insure_appli = #{userId} order by gu.update_time desc
```
  
---

### 9.查看申请投保
#### 基本信息
     请求类型：HTTP
     请求地址：http://127.0.0.1:8080/policy/viewApplyPolicy
     请求方式：get
     请求类型：String ,String
     响应类型：R
#### 接口描述
     本接口是查询企业的投保信息
     1.如果userId为null或者“”，抛出异常
     2.如果没有数据，返回无数据
#### 请求数据
   <table>
        <tr>
            <th>参数名称</th>
            <th>是否必填</th>
            <th>描述</th>
            <th>默认值</th>
        </tr>  
        <tr>
            <td>businessNo</td>
            <td>√</td>
            <td>申请id</td>
            <td></td>
        </tr>   
        <tr>
            <td>token</td>
            <td>√</td>
            <td>登录验证</td>
            <td></td>
        </tr>
    </table>
#### 响应数据
   <table>
       <tr>
           <th>参数名称</th>
           <th>是否必填</th>
           <th>描述</th>
           <th>默认值</th>
       </tr>  
       <tr>
           <td>data</td>
           <td>√</td>
           <td>map对象</td>
           <td></td>
       </tr>   
   </table> 
#### 实例
  请求参数：  
  {
     "businessNo":"zhangsan",
     "token":"154dfsdff48313s1ve844313131fsd8"
  }  
   响应参数： 
```json 
{
  "code":200,  
   "msg":"success",  
   "data":  
  {  
    
  }
}  
```
#### 数据库操作
   根据userId查询投保列表  
```sql
    ### 保单基本信息
   select gu.business_no,gc.corp_name appli_name,gc.uniform_code,gc.province,gc.city,gc.county,gc.town,gc.village,gc.address,gc.identity_no,gs.concat,gs.post_code,go.organ_name,go.identity_no insured_identity_no,gs.contact,go.mobile insured_mobile,gs.address,go.organ_name,gp.product_name risk_name,gu.amount,(select organ_name from ggorgan where organ_id = gu.insurance_code) insurance_code,gu.letter_id
     from gupolicymain gu, ggproduct gp ,ggusercorp gc,ggorgan go,gguser gs  where gu.business_no = #{businessNo} and gp.product_id = gu.risk_code and gc.user_id = gu.appli_code go.organ_id = gu.insured_code and gu.appli_code = gs.user_id and gu.status = '5' 
    #### 投保人配偶
    根据主键businessNo查询
    #### 推荐函
    根据主键letter_id查询
    ### 资证
    select card_name，gu.corp_name ,card_type，card_no，end_date，card_img from ggmanagercard gm ，ggusercorp gu where 


```

### 3.机构查询接口
#### 基本信息
请求类型： http
请求地址： http://ip/organ/listOrgans
请求方式： get
参数类型： String，String
响应类型： R

#### 接口描述
本接口是查询申请贷款、申请投保、申请担保时查询机构

#### 请求参数
<table>
    <tr>
        <th>参数名称</th>
        <th>是否必填</th>
        <th>描述</th>
        <th>默认值</th>
    </tr>  
    <tr>
        <td>organType</td>
        <td>√</td>
        <td>机构类型（1保险公司，2信贷公司，3担保公司，4其他）</td>
        <td></td>
    </tr>   
    <tr>
        <td>token</td>
        <td>√</td>
        <td>登录验证</td>
        <td></td>
    </tr>
</table>

#### 响应数据
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>organList</td>
       <td>√</td>
       <td>map集合</td>
       <td></td>
   </tr>   
</table> 

#### 实例
请求参数  
```json
 {
     "organType":"1",
     "token":"154dfsdff48313s1ve844313131fsd8"
  }  
```
响应数据  
1.成功
```json
{
  "code":200,  
   "msg":"success",  
   "organList":  
  :[  
     {  
      "organ_id":"1236478910",  
      "organ_name":"保险公司"
    },
    {  
      "organ_id":"1236478910",
      "organ_name":"保险公司"
    }  
   ]
  
}  
```
2.失败
```json
{
  "code":500,  
   "msg":"查询失败"
}  
```
#### 数据库操作
```sql
select organ_id,organ_name from ggorgan where organ_type = #{organType} and valid_status = '1'
```
---
### 4.查询产品
#### 基本信息
请求类型： http
请求地址： http://ip/product/listProducts
请求方式： get
参数类型： String ，String
响应类型： R
#### 接口描述
根据机构查询产品

#### 请求参数
<table>
  <tr>
      <th>参数名称</th>
      <th>是否必填</th>
      <th>描述</th>
      <th>默认值</th>
  </tr>  
  <tr>
      <td>organId</td>
      <td>√</td>
      <td>机构代码</td>
      <td></td>
  </tr>   
  <tr>
      <td>token</td>
      <td>√</td>
      <td>登录验证</td>
      <td></td>
  </tr>
</table>
#### 响应数据
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>productList</td>
       <td>√</td>
       <td>map集合</td>
       <td></td>
   </tr>   
</table> 
#### 实例
请求参数
```json
{
   "organId":"1",
   "token":"154dfsdff48313s1ve844313131fsd8"
} 
```
响应数据
1.成功
```json
{
  "code":200,  
   "msg":"success",  
   "productList":  
  :[  
     {  
      "product_id":"1236478910",  
      "product_name":"流动贷款"
    },
    {  
      "product_id":"1236478910",
      "product_name":"流动贷款"
    }  
   ]
  
}  
```
2.失败
```json
{
  "code":500,  
   "msg":"查询失败"
}  
```
#### 数据库操作
```sql
select product_id,product_name from ggproduct where company_code = #{organId} and valid_status = '1'
```
### 5.查询产品详情接口
#### 基本信息
请求类型： http
请求地址： http://ip/product/getProductDetail
请求方式： get
参数类型： String ，String
响应类型： R
#### 接口描述
根据产品id查询产品详情
#### 请求参数
<table>
  <tr>
      <th>参数名称</th>
      <th>是否必填</th>
      <th>描述</th>
      <th>默认值</th>
  </tr>  
  <tr>
      <td>productId</td>
      <td>√</td>
      <td>产品代码</td>
      <td></td>
  </tr>   
  <tr>
      <td>token</td>
      <td>√</td>
      <td>登录验证</td>
      <td></td>
  </tr>
</table>
#### 响应数据
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>productDetail</td>
       <td>√</td>
       <td>productDetail</td>
       <td></td>
   </tr>   
</table> 
#### 实例
请求参数
```json
{
   "productId":"461561166",
   "token":"154dfsdff48313s1ve844313131fsd8"
} 
```
响应数据
1.成功
```json
{
  "code":200,  
   "msg":"success",  
   "productDetail":  
    {  
      "flag":"",  
      "payType":"",
      "productIntroduce":"",
      "productId":"",
      "rate":0,
      "infomation":"",
      "loanArrange":"",
      "productImg":"",
      "remark":"",
      "loanAmount":"",
      "productDes":""
    }
}  
```
2.失败
```json
{
  "code":500,  
   "msg":"查询失败"
}  
```
#### 数据库操作
```sql
select * from ggproductdetail where product_id = #{productId} and valid_status = '1'
```

### 6.查询是否有草稿接口
#### 基本信息
请求类型： http  
请求地址： http://ip/policy/getSavedData  
请求方式： get  
参数类型： String ，String  
响应类型： R  
#### 接口描述
根据用户id查询是否存在草稿
#### 请求参数
<table>
  <tr>
      <th>参数名称</th>
      <th>是否必填</th>
      <th>描述</th>
      <th>默认值</th>
  </tr>  
  <tr>
      <td>userId</td>
      <td>√</td>
      <td>用户代码</td>
      <td></td>
  </tr>   
  <tr>
      <td>token</td>
      <td>√</td>
      <td>登录验证</td>
      <td></td>
  </tr>
</table>
#### 响应数据
1.不存在草稿
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>data</td>
       <td>√</td>
       <td>信息为null</td>
       <td></td>
   </tr>   
</table> 
2.存在草稿
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>data</td>
       <td>√</td>
       <td>投保信息，配偶信息，申请资料信息</td>
       <td></td>
   </tr>   
</table> 
#### 实例
请求参数
```json
{
   "userId":"461561166",
   "token":"154dfsdff48313s1ve844313131fsd8"
} 
```
响应数据
1.存在草稿
```json
{
  "code":200,  
   "msg":"success",  
   "data":  
    {
      "guPolicyMain":
      {
        "arbitrationCommision":"",
        "flag":"",
        "endDate":null,
        "disputeType":"",
        "inputTime":null,
        "policyNo":"",
        "remark":"",
        "insuranceCode":"",
        "businessNo":"",
        "premium":0,
        "recordAddress":"",
        "rate":0,
        "excess":0,
        "amount":0,
        "insurancePath":"",
        "riskCode":"",
        "updateTime":null,
        "broker":"",
        "insureAppli":"",
        "proposalNo":"",
        "insuredCode":"",
        "beneficiary":"",
        "contractId":"",
        "letterId":"",
        "updator":"",
        "startDate":null,
        "status":""
      },
      "guPolicyMate":
      {
        "identityNo":"",
        "businessNo":"",
        "flag":"",
        "companyName":"",
        "businessClassCode":"",
        "mobile":"",
        "name":"",
        "remark":""
      },
      "guApplyData":
      {
        "applyId":"",
        "flag":"",
        "otherId":"",
        "contractIds":"",
        "assetIds":"",
        "managerCards":"",
        "remark":"",
        "financialIds":"",
        "invoiceIds":""
      }
  }
}  
```
2.不存在草稿
```json
{
  "code":200,  
   "msg":"success"，
   "data": null
}  
```
### 7.投保申请提交接口
#### 基本信息
请求类型： http
请求地址： http://ip/policy/savePolicy
请求方式： post
参数类型： gupolicymain，gupolicymate，guapplydata
响应类型： R
#### 接口描述
根据用户id查询是否存在草稿
#### 请求参数
<table>
  <tr>
      <th>参数名称</th>
      <th>是否必填</th>
      <th>描述</th>
      <th>默认值</th>
  </tr>  
  <tr>
      <td>gupolicymain</td>
      <td>√</td>
      <td>gupolicymain的字段值</td>
      <td></td>
  </tr>   
  <tr>
      <td>gupolicymate</td>
      <td>√</td>
      <td>gupolicymate的字段值</td>
      <td></td>
  </tr>  
  <tr>
      <td>guapplydata</td>
      <td>√</td>
      <td>guapplydata的字段值</td>
      <td></td>
  </tr>  
  <tr>
      <td>token</td>
      <td>√</td>
      <td>登录验证</td>
      <td></td>
  </tr>
</table>
#### 响应数据
1.成功
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>msg</td>
       <td>√</td>
       <td>success</td>
       <td></td>
   </tr>   
</table> 
2.失败
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>msg</td>
       <td>√</td>
       <td>error</td>
       <td></td>
   </tr>   
</table> 
#### 实例
请求参数
```json
{
  "arbitrationCommision":"",
  "flag":"",
  "endDate":null,
  "disputeType":"",
  "inputTime":null,
  "policyNo":"",
  "remark":"",
  "insuranceCode":"",
  "premium":0,
  "recordAddress":"",
  "rate":0,
  "excess":0,
  "amount":0,
  "insurancePath":"",
  "riskCode":"",
  "updateTime":null,
  "broker":"",
  "insureAppli":"",
  "proposalNo":"",
  "insuredCode":"",
  "beneficiary":"",
  "contractId":"",
  "letterId":"",
  "updator":"",
  "startDate":null,
  "status":"",

  "identityNo":"",
  "flag":"",
  "companyName":"",
  "businessClassCode":"",
  "mobile":"",
  "name":"",
  "remark":"",

  "flag":"",
  "otherId":"",
  "contractIds":"",
  "assetIds":"",
  "managerCards":"",
  "remark":"",
  "financialIds":"",
  "invoiceIds":""
}
```
响应数据  
1.成功
```json
{
  "code":200,  
   "msg":"success"  
}  
```
2.失败
```json
{
  "code":500,  
   "msg":"error"
}  
```

### 8.我的保单接口
请求类型： http  
请求地址： http://ip/policy/listPolicys  
请求方式： get  
参数类型： String，String  
响应类型： R  
#### 接口描述
根据用户id查询是否存在草稿
#### 请求参数
<table>
  <tr>
      <th>参数名称</th>
      <th>是否必填</th>
      <th>描述</th>
      <th>默认值</th>
  </tr>  
  <tr>
      <td>userId</td>
      <td>√</td>
      <td>投保人id</td>
      <td></td>
  </tr>    
  <tr>
      <td>token</td>
      <td>√</td>
      <td>登录验证</td>
      <td></td>
  </tr>
</table>
#### 响应数据  
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>page</td>
       <td>√</td>
       <td>分页对象</td>
       <td></td>
   </tr>   
</table> 
#### 实例
请求参数
```json
{
  "userId":"123456",
  "token":"dfaafd45486d165484s6d646"
}
```
响应数据  
1.成功
{
  "code":200,  
   "msg":"success",  
   "page":  
  {  
     "total":0,  
      "pages":0,  
      "size":1,  
      "pageSize":0,  
     "policyList":[  
               {  
                 "amount":50000,  
                 "rate":0.02,  
                 "input_time":{  
                      "date":5,  
                      "hours":14,  
                      "seconds":29,  
                      "month":0,  
                      "timezoneOffset":-480,  
                      "year":118,  
                      "minutes":15,  
                      "time":1515132929635,  
                      "day":5  
                    },  
                 "business_no":"1236478999",  
                 "risk_code":"123", 
                 "risk_name":"123", 
                 "status":"5"  
               }  
             ],   
         "pageNum":0  
  }
}  
```
2.失败
```json
{
  "code":500,  
   "msg":"error"
}  
```
#### 数据库操作
  根据userId查询投保列表  
```sql
  select gu.business_no,gu.risk_code,gp.product_name risk_name,gu.amount,gu.rate,gu.input_time,gu.status   
     from gupolicymain gu left join ggproduct gp on gu.risk_code= gp.product_id  where gu.insure_appli = #{userId} and gu.status = '5' order by gu.update_time desc
```
### 9.保单查看接口
请求类型： http  
请求地址： http://ip/policy/viewPolicyDetail  
请求方式： get  
参数类型： String，String  
响应类型： R  
#### 接口描述
根据用户id查询是否存在草稿
#### 请求参数
<table>
  <tr>
      <th>参数名称</th>
      <th>是否必填</th>
      <th>描述</th>
      <th>默认值</th>
  </tr>  
  <tr>
      <td>businessNo</td>
      <td>√</td>
      <td>保单id</td>
      <td></td>
  </tr>    
  <tr>
      <td>token</td>
      <td>√</td>
      <td>登录验证</td>
      <td></td>
  </tr>
</table>
#### 响应数据  
<table>
   <tr>
       <th>参数名称</th>
       <th>是否必填</th>
       <th>描述</th>
       <th>默认值</th>
   </tr>  
   <tr>
       <td>policy</td>
       <td>√</td>
       <td>map对象</td>
       <td></td>
   </tr>   
</table> 
#### 实例
请求参数
```json
{
  "businessNo":"123456",
  "token":"dfaafd45486d165484s6d646"
}
```
响应数据  
1.成功
```json
{
  "code":200,  
   "msg":"success",  
   "policy":  
  {  
     "insured_identity_no":""
      "end_date":null,
      "dispute_type":""
      "policy_no":""
      "insurance_code":"",
      "premium":0,
      "recordAddress":"",
      "rate":0,
      "excess":0,
      "amount":0,
      "insurancePath":"",
      "risk_name":"",
      "broker":"",
      "appli_name":"",
      "policy_no":"",
      "organ_name":"",
      "insurance_code":"",
      "insured_mobile":"",
      "insurance_path":""
      "start_date":null
  }
}  
```
2.失败
```json
{
  "code":500,  
   "msg":"error"
}  
```
#### 数据库操作
  根据userId查询投保列表  
```sql
  select gu.business_no,gu.policy_no,gc.corp_name appli_name,go.organ_name,gc.uniform_code,go.identity_no insured_identity_no,gs.contact,go.mobile insured_mobile,gs.address,go.organ_name,gp.product_name risk_name,gu.amount,gu.rate,gu.premium,gu.start_date,gu.end_date,gu.excess,gu.dispute_type,gu.insurance_path,(select organ_name from ggorgan where organ_id = gu.insurance_code) insurance_code,gu.broker 
     from gupolicymain gu, ggproduct gp ,ggusercorp gc,ggorgan go,gguser gs  where gu.business_no = #{business_no} and gp.product_id = gu.risk_code and gc.user_id = gu.appli_code go.organ_id = gu.insured_code and gu.appli_code = gs.user_id and gu.status = '5' 

  ###推荐函  根据gu.letter_id查询
  ###借款合同  根据gu.contract_id查询
```
