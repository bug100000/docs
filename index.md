## 同行文档



## 产品设计




## 前端



## 后端




## 数据库



数据表名称	字段名称	类型	是否必填	字段说明	实例
tx_user(用户基本信息表)	user_id	string(32)	是	用户系统id	23213433453453453453425435657001
	user_phone	string(16)	否	用户手机号	12345678909
	user_nick_name	string(32)	否	用户昵称	李先生
	user_sex	int(1)	否	用户性别	0男 1女 2未知
	user_wx_id	string(32)	否	用户微信id	wx123034539456456234231
	user_wx_portriat	string(32)	是	用户微信头像链接	https://imgs.wx.com/userId=asdasd32432432
	user_wx_name	string(32)	是	用户微信昵称	三生三世
	user_level	int(2)	是	用户级别	默认1
	user_score	int(32)	是	用户积分	默认1
	user_focus_other	string(128)	是	用户关注的其他用户	默认为'', 其他值"1,2,3,4"id号的序列
	user_focus_self	string(128)	是	被这些用户关注	默认为'', 其他值"5,6,7,8"id号序列
	user_create_time	string(32)	是	用户账号创建时间	"2017-05-12 13:23:30"
	user_last_login_time	string(32)	是	用户最后一次登录时间	"2018-05-27 16:23:00"
	user_agent	string(32)	是	用户设备信息	"Android4.0.0"
	user_disabled_end_time	string(32)	是	用户禁止发布的截止时间	'表示没有禁止，'2018-05-27 14:33:35'表示截止时间点
	user_active	int(1)	是	当前账号是否可用	1(默认 可用) 0(不可用)
tx_trip(用户行程表)	trip_id	string(32)	是	行程记录id	42345435435452535654768708076865
	trip_start_location	string(32)	是	出发地	北京'
	trip_end_location	string(32)	是	目的地	青岛'
	trip_start_time	string(32)	是	行程开始时间	2018-05-28 08:30'
	trip_end_time	string(32)	是	行程结束时间	2018-05-30 18:30'
	trip_merber_count	int(8)	是	行程团队人数	5
	trip_other_desc	string(128)	否	行程要求	默认'', '有车有房'
	trip_status	int(2)	是	行程状态	-1(草稿) 0正常等待 1进行中 2完成 3过期'
	trip_publish_user_id	string(32)	是	发起人的用户id	23423423
	trip_create_time	string(32)	是	行程创建时间	"2018-05-30 18:30:23"
	trip_request_user_info	string(128)	是	请求参团的用户id列表	默认"0", "['213123','23435345','5654765]"请求加入则push，拒绝则splice，同意则splice并转到下一字段
	trip_active	int(1)	是	当前行程状态	默认1(可用) 0(不可用)
	trip_merber_info	string(256)	是	参与行程成员的信息	[{"user_id":"1","user_wx_portriat":"https://imgs.wx.com/userid=23425","sign": 1,"sign_self":1}]'发起人确认签到，自己签到
tx_trip_comment(行程中对团员的评论)	trip_comment_id	string(32)	是	评论id	1232342346509856
	trip_comment_trip_id	string(32)	是	行程id	23543254354
	trip_comment_from_user_id	string(32)	是	评论发起方用户id	
	trip_comment_to_user_id	string(32)	是	评论接受方用户id	
	trip_comment_content	string(128)	是	评论内容	"评论内容"
	trip_comment_create_time	string(32)	是	评论创建时间	"2018-05-28 16:55:30"
	trip_comment_active	int(1)	是	评论是否可用	默认1(可用) 0(不可用)
tx_enter_page_log(用户进入页面的记录)	enter_page_id	string(32)	是	记录id	
	enter_page_page_id	string(16)	是	页面的唯一标记	index', 'person_home'
	enter_page_view_user_id	string(32)	是	进入当前页面的用户id	
	enter_page_start_time	string(16)	是	进入当前页面的时间	
	enter_page_end_time	string(16)	否	离开页面的时间	
tx_search_word_log(用户搜索词记录)	search_word_id	string(32)	是	记录id	
	search_word_user_id	string(32)	是	用户id	
	search_word_keyword	string(64)	是	用户搜索的热词	
	search_word_create_time	string(16)	是	搜索的时间	
