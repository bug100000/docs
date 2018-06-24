**与我同行一期接口文档**

**1.所有的页面标识**

首页: index

约伴详情页: trip\_detail

发布页: trip\_publish

个人主页: personal\_home

> 我的发起: personal\_publish
>
> 我的同行: personal\_tx
>
> 我的草稿: personal\_draft
>
> 申请记录: personal\_apply

1.  **日志控制:**

    **请求的日志:(logs/api.req.log)**

> **前端**调用接口时需要在**请求header**中添加如下字段:

1.  uid: 当前用户id

2.  page: 当前页面唯一标识(如上)

3.  platform: 请求来自的平台

> **后端**获取上述header中的字段，并且
>
> 获取header中自身携带的以下字段:

1.  IP地址

2.  user\_agent用户设备

3.  method请求的方法

> 后端获取请求的当前系统时间localTime
>
> 后端生成的唯一标识

**响应的日志:(logs/api.res.log)**

> 响应的当前系统时间localTime
>
> 响应状态码
>
> 响应数据
>
> 后端生成的唯一标识(与请求对应)

**日志实例：**

1.  请求日志:

格式: 标识\|请求时间\|IP\|页面标识\|请求url\|请亲方式\|uid\|platform\|user\_agent

实例: dee1a820-6644-11e8-b6a2-9b929de148c9\|2018-06-02T17:11:01+08:00\|192.168.43.208\|index\|/api/index\|POST\|1245\|wechat\|PostmanRuntime/7.1.5

1.  响应日志:

格式: 标识\|响应时间\|响应状态\|响应数据

实例: 33e38e70-6653-11e8-9fad-b3f25a9f6505\|2018-06-02T18:53:37+08:00\|404\|{"code":40004,"msg":"资源不存在"}

1.  **api接口请求**

    **请求的整体结构**

> **请求: **
>
> url: ‘/api/searchKey’,
>
> header: 添加规定的条件,
>
> type: ‘post’,
>
> data: {
>
> key: val
>
> }
>
> **响应:(响应的body部分)**
>
> **http状态码为200情况下:**
>
> {
>
> code: ‘2000’,
>
> msg: ‘success’,
>
> data: { // 这里存放的数据详细
>
> }
>
> }

**3.1首页**

**3.1.1**依据关键词搜索相关行程

|          |                             |                           |                     |
|----------|-----------------------------|---------------------------|---------------------|
| 请求     |                             |                           |                     |
| Url      | /v1/queryTripListByWord     |                           |                     |
| Method   | POST                        |                           |                     |
|          | currentPage                 | 当前搜索的页数            | 如 “1”              |
|          | pageSize                    | 每页显示的条数            | 如 “10”, 先默认为10 |
| Data     | keyword                     | 搜索的词                  | 如 “故宫”           |
| 响应     |                             |                           |                     |
| tripList | 满足搜索条件的行程列表      | \[ \]数组                 |                     |
| {}       | publish\_user\_id           | 发起人id                  |                     |
|          | publish\_user\_wx\_name     | 发起人昵称                |                     |
|          | publish\_user\_wx\_portriat | 发起人头像地址            |                     |
|          | trip\_create\_time          | 行程创建时间 ‘2018-02-03’ |                     |
|          | trip\_end\_location         | 目的地 ‘故宫’             |                     |
|          | trip\_start\_time           | 开始时间 ‘2018-03-23’     |                     |
|          | trip\_end\_time             | 结束时间 ‘2018-03-25’     |                     |
|          | trip\_merber\_count         | 行程人数                  |                     |
|          | trip\_id                    | 行程id号                  |                     |

说明: 这里请求在发送至后台时，后台需要1.拿取传递的数据，搜索相关记录(mysql) 2.将搜索词记录在热词日志中

**3.1.2**行程分页查询(刚进入首页其实是查询第一页的内容，依据触发日期先后)

|          |                             |                           |                     |
|----------|-----------------------------|---------------------------|---------------------|
| 请求     |                             |                           |                     |
| Url      | /v1/queryTripListByWord     |                           |                     |
| Method   | POST                        |                           |                     |
| Data     | currentPage                 | 当前搜索的页数            | 如 “1”              |
|          | pageSize                    | 每页显示的条数            | 如 “10”, 先默认为10 |
|          | keyword                     | 当前搜索词                | 默认为’’            |
| 响应     |                             |                           |                     |
| tripList | 满足搜索条件的行程列表      | \[ \]数组                 |                     |
|          | publish\_user\_id           | 发布人id                  |                     |
|          | publish\_user\_wx\_name     | 发起人昵称                |                     |
|          | publish\_user\_wx\_portriat | 发起人头像地址            |                     |
|          | trip\_create\_time          | 行程创建时间 ‘2018-02-03’ |                     |
|          | trip\_end\_location         | 目的地 ‘故宫’             |                     |
|          | trip\_start\_time           | 开始时间 ‘2018-03-23’     |                     |
|          | trip\_end\_time             | 结束时间 ‘2018-03-25’     |                     |
|          | trip\_merber\_count         | 行程人数                  |                     |
|          | trip\_id                    | 行程id                    |                     |

说明: 当keyword为””时，后端直接从缓存中拿取相关数据即可。

**3.2约伴详情页**

**3.2.1**依据行程id查询详细信息

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/queryTripDetail</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>trip_id</td>
<td>行程id</td>
<td>如 “sdfd32424”</td>
</tr>
<tr class="odd">
<td></td>
<td>user_id</td>
<td>当前用户id</td>
<td></td>
</tr>
<tr class="even">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>publish_user_id</td>
<td>发起人id</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>publish_user_wx_name</td>
<td>发起人昵称</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>publish_user_wx_portriat</td>
<td>发起人头像地址</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_create_time</td>
<td>行程创建时间 ‘2018-02-03’</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_start_location</td>
<td>出发地</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_end_location</td>
<td>目的地 ‘故宫’</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_start_time</td>
<td>开始时间 ‘2018-03-23’</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_end_time</td>
<td>结束时间 ‘2018-03-25’</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_member_count</td>
<td>行程人数</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_member_info</td>
<td><p>同行人的信息 数组</p>
<p>[{user_id:’’,user_wx_portriat:’’}]</p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_other_desc</td>
<td>行程要求</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_status</td>
<td>行程状态</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_id</td>
<td>行程id号</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>apply_status_to_add</td>
<td><p>当前用户对于此行程的状态</p>
<p>0申请中 1同意 2拒绝</p></td>
<td></td>
</tr>
</tbody>
</table>

说明: 后端需要查询两张表: 行程基本信息表, 申请记录表(主要确定apply\_status\_to\_add字段的值)，这里两者没有先后依赖关系，建议promise.all同时查询(async/await只在存在先后依赖关系使用)

**3.2.2**申请参团

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/requestJoin</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>trip_id</td>
<td>行程id</td>
<td>如 “sdfd32424”</td>
</tr>
<tr class="odd">
<td></td>
<td>user_id</td>
<td>加入人id</td>
<td>如 “sdf343”</td>
</tr>
<tr class="even">
<td></td>
<td>publisher_id</td>
<td>发布人id</td>
<td></td>
</tr>
<tr class="odd">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>请求成功变为”等待同意中...”</p>
<p>这里依据code码即可判断</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

说明: 后端在插入记录时需要判断是否有匹配当前信息的记录，如果存在并且为申请中...则不插入，并返回前端”你已申请”的code(20002)

**3.2.3**获取申请列表(对于发起人)

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/queryTripApplyList</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>trip_id</td>
<td>行程id</td>
<td>如 “sdfd32424”</td>
</tr>
<tr class="odd">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>applyList</td>
<td>满足搜索条件的行程列表</td>
<td>[ ]数组</td>
<td></td>
</tr>
<tr class="odd">
<td>{}</td>
<td>apply_trip_id</td>
<td>申请的行程id</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>apply_user_id</td>
<td>申请人id</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>apply_user_info</td>
<td><p>申请人基本信息</p>
<p>{user_id:用户id’’,user_wx_name:’昵称’,user_wx_portriat:’头像’}</p></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>apply_status_to_add</td>
<td><p>申请状态</p>
<p>0申请中 1同意 2拒绝</p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>apply_create_time</td>
<td><p>申请日期</p>
<p>2018-06-03 12:54</p></td>
<td></td>
</tr>
</tbody>
</table>

**3.2.3**发布人同意参团

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/agreeJoin</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>trip_id</td>
<td>行程id</td>
<td>如 “sdfd32424”</td>
</tr>
<tr class="odd">
<td></td>
<td>user_id</td>
<td>加入人id</td>
<td>如 “sdf343”</td>
</tr>
<tr class="even">
<td></td>
<td>publisher_id</td>
<td>发布人id</td>
<td></td>
</tr>
<tr class="odd">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>请求成功变为”等待同意中...”</p>
<p>这里依据code码即可判断</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

说明: 后端需要同时操作两张表，使用mysql的事务，操作行程基本信息表(添加同意的人)，与申请记录表(修改记录状态)

**3.2.4**发布人不同意参团

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/notAgreeJoin</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>trip_id</td>
<td>行程id</td>
<td>如 “sdfd32424”</td>
</tr>
<tr class="odd">
<td></td>
<td>user_id</td>
<td>加入人id</td>
<td>如 “sdf343”</td>
</tr>
<tr class="even">
<td></td>
<td>publisher_id</td>
<td>发布人id</td>
<td></td>
</tr>
<tr class="odd">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>请求成功变为”等待同意中...”</p>
<p>这里依据code码即可判断</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

说明: 后端只需要操作申请记录表(修改记录状态)

**3.2.5**退出

|                                                                |               |          |                |
|----------------------------------------------------------------|---------------|----------|----------------|
| 请求                                                           |               |          |                |
| Url                                                            | /v1/leave     |          |                |
| Method                                                         | POST          |          |                |
| Data                                                           | trip\_id      | 行程id   | 如 “sdfd32424” |
|                                                                | user\_id      | 申请人id | 如 “sdf343”    |
|                                                                | publisher\_id | 发布人id |                |
| 响应                                                           |               |          |                |
| 请求成功，直接操作数据，如果返回成功则直接改变状态为”申请参团” |               |          |                |
|                                                                |               |          |                |

说明: 后端在插入记录时需要判断是否有匹配当前信息的记录，并且为已经退出.则不插入，并返回前端”你已退出”的code(20003); 如果可以退出，则同样需要mysql事务同时操作行程记录表与申请记录表

**3.2.6**在当前行程下评论团中其他人

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/merberComment</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>trip_id</td>
<td>行程id</td>
<td>如 “sdfd32424”</td>
</tr>
<tr class="odd">
<td></td>
<td>trip_end_location</td>
<td>行程结束目的地</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_end_time</td>
<td>行程结束日期</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>user_id</td>
<td>评论人id</td>
<td>如 “sdf343”</td>
</tr>
<tr class="even">
<td></td>
<td>to_user_id</td>
<td>被评论人id</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>content</td>
<td>评论内容</td>
<td></td>
</tr>
<tr class="even">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td><p>请求成功变为”等待同意中...”</p>
<p>这里依据code码即可判断</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

**4.发布页面**

**4.1** 发布行程

|                  |                         |          |                  |
|------------------|-------------------------|----------|------------------|
| 请求             |                         |          |                  |
| Url              | /v1/publishTrip         |          |                  |
| Method           | POST                    |          |                  |
| Data             | trip\_start\_location   | 出发地   |                  |
|                  | trip\_end\_location     | 目的地   |                  |
|                  | trip\_start\_time       | 开始时间 |                  |
|                  | trip\_end\_time         | 结束时间 |                  |
|                  | trip\_merber\_count     | 团队人数 | 包括发起者的人数 |
|                  | trip\_other\_desc       | 行程要求 |                  |
|                  | trip\_publish\_user\_id | 发起人id |                  |
| 响应             |                         |          |                  |
| 结果依据code判断 |                         |          |                  |
|                  |                         |          |                  |

**4.2** 编辑发布(包括我的草稿)

|                  |                         |          |                  |
|------------------|-------------------------|----------|------------------|
| 请求             |                         |          |                  |
| Url              | /v1/saveTrip            |          |                  |
| Method           | POST                    |          |                  |
| Data             | trip\_start\_location   | 出发地   |                  |
|                  | trip\_end\_location     | 目的地   |                  |
|                  | trip\_start\_time       | 开始时间 |                  |
|                  | trip\_end\_time         | 结束时间 |                  |
|                  | trip\_merber\_count     | 团队人数 | 包括发起者的人数 |
|                  | trip\_other\_desc       | 行程要求 |                  |
|                  | trip\_publish\_user\_id | 发起人id |                  |
|                  | trip\_id                | 行程id   |                  |
| 响应             |                         |          |                  |
| 结果依据code判断 |                         |          |                  |
|                  |                         |          |                  |

**5.我的发起页，我的同行页**

**5.1** 依据user\_id获取用户发起的行程记录

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/queryMyPublish /v1/queryMyTx</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>user_id</td>
<td>用户id</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>currentPage</td>
<td>当前页</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>pageSize</td>
<td>每页显示的数量</td>
<td>默认10</td>
</tr>
<tr class="odd">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>tripList</td>
<td>列表信息</td>
<td>[]数组</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>user_wx_name</td>
<td>用户昵称 ‘张三’</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>user_wx_portriat</td>
<td>用户头像连接 ‘htpps://’</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_create_time</td>
<td>行程创建时间 ‘2018-02-03’</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_end_location</td>
<td>目的地 ‘故宫’</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_start_time</td>
<td>开始时间 ‘2018-03-23’</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_end_time</td>
<td>结束时间 ‘2018-03-25’</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_merber_count</td>
<td>行程人数</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_id</td>
<td>行程id</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_status</td>
<td>行程状态</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_merber_info</td>
<td><p>参团人的信息</p>
<p>'[{&quot;user_id&quot;:&quot;1&quot;,&quot;user_wx_portriat&quot;:&quot;https://imgs.wx.com/userid=23425&quot;}]'</p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_has_news</td>
<td><p>是否有新状态</p>
<p>0 / 1</p></td>
<td></td>
</tr>
</tbody>
</table>

说明：我的发布与我的同行都是搜索行程基本信息表(根据行程发布先后)，联表查询申请记录表来确定trip\_has\_new

**6.我的草稿**

**6.1**依据user\_id查询trip\_status = 0的记录

|          |                       |                           |        |
|----------|-----------------------|---------------------------|--------|
| 请求     |                       |                           |        |
| Url      | /v1/queryMyDraftList  |                           |        |
| Method   | POST                  |                           |        |
| Data     | user\_id              | 用户id                    |        |
|          | currentPage           | 当前页                    |        |
|          | pageSize              | 每页显示的数量            | 默认10 |
| 响应     |                       |                           |        |
| tripList | 列表信息              | \[\]数组                  |        |
|          | trip\_create\_time    | 行程创建时间 ‘2018-02-03’ |        |
|          | trip\_start\_location | 出发地                    |        |
|          | trip\_end\_location   | 目的地 ‘故宫’             |        |
|          | trip\_start\_time     | 开始时间 ‘2018-03-23’     |        |
|          | trip\_end\_time       | 结束时间 ‘2018-03-25’     |        |
|          | trip\_merber\_count   | 行程人数                  |        |
| Trip     | trip\_other\_desc     | 行程要求                  |        |
|          | trip\_id              | 行程id                    |        |

这里点击继续编辑跳转至发布页面，前端接受相关数据到发布页面

**7.申请记录页面(我申请)**

7.1依据user\_id查询

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/queryMyRequestList</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>user_id</td>
<td>用户id</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>currentPage</td>
<td>当前页</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>pageSize</td>
<td>每页显示的数量</td>
<td>默认10</td>
</tr>
<tr class="odd">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>tripList</td>
<td>列表信息</td>
<td>[]数组</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_id</td>
<td>行程id</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_start_location</td>
<td>出发地</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_end_location</td>
<td>目的地 ‘故宫’</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_start_time</td>
<td>开始时间 ‘2018-03-23’</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_end_time</td>
<td>结束时间 ‘2018-03-25’</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>apply_status_to_add</td>
<td>申请状态</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>apply_status_to_publisher</td>
<td>对于发起人是否有新状态</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>apply_status_to_user</td>
<td>对于参加人是否有新状态</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_publish_user_info</td>
<td><p>发起人的相关信息</p>
<p>'[{&quot;user_id&quot;:&quot;1&quot;,&quot;user_wx_portriat&quot;:&quot;https://imgs.wx.com/userid=23425&quot;},&quot;user_wx_name&quot;:'张三']'</p></td>
<td></td>
</tr>
</tbody>
</table>

**8.对我的评论**

<table>
<tbody>
<tr class="odd">
<td>请求</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Url</td>
<td>/v1/queryCommentToMe</td>
<td></td>
<td></td>
</tr>
<tr class="odd">
<td>Method</td>
<td>POST</td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>Data</td>
<td>user_id</td>
<td>当前用户id</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>currentPage</td>
<td>当前页</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>pageSize</td>
<td>每页显示的数量</td>
<td>默认10</td>
</tr>
<tr class="odd">
<td>响应</td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td>tripList</td>
<td>列表信息</td>
<td>[]数组</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_comment_id</td>
<td>评论id</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_comment_from_user_info</td>
<td><p>评论发起人信息</p>
<p>{user_id:'',user_wx_name:'',user_wx_portriat:''}</p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_comment_content</td>
<td>评论内容</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_comment_create_time</td>
<td>评论时间</td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td>trip_end_time</td>
<td>结束时间 ‘2018-03-25’</td>
<td></td>
</tr>
<tr class="even">
<td></td>
<td>trip_comment_trip_info</td>
<td><p>评论对应的行程概述信息</p>
<p>{trip_id:'',trip_end_location:'',trip_end_time:''}</p></td>
<td></td>
</tr>
</tbody>
</table>

**9.个人主页和首页**

在进入页面后需要查询当前用户是否有新状态未处理，这里需要调用接口查询，然后在相关位置展示红点

|        |               |                              |     |
|--------|---------------|------------------------------|-----|
| 请求   |               |                              |     |
| Url    | /v1/myNews    |                              |     |
| Method | POST          |                              |     |
| Data   | user\_id      | 用户id                       |     |
| 响应   |               |                              |     |
|        | trip\_apply   | 1/0 表示是否申请状态有新状态 |     |
|        | trip\_publish | 1/0 我的发布有新状态         |     |
|        | trip\_comment | 1/0 是否有新评论             |     |

后期：在首页查询一次是否有新状态，表示红点；在进入”我的”时需要查询不同模块的新状态的数量统计。

**10.页面标识接口**
页面标识每个页面对应的值，见文档最上头

|        |               |                              |     |
|--------|---------------|------------------------------|-----|
| 请求   |               |                              |     |
| Url    | /v1/pageSign   |                              |     |
| Method | POST          |                              |     |
| 响应   |               |                              |     |
|        | trip\_code   |          20000                |     |
|        | trip\_msg    |            success            |     |

