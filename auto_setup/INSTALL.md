#常见部署方案
	假设所有服务都部署在一台机器上

###1.纯公司内网 
	安装的机器内网ip为：  108.160.141.216
	
**login_server:**

	ClientListenIP= 108.160.141.216		
	ClientPort=8008
	HttpListenIP= 108.160.141.216
	HttpPort=8080
	MsgServerListenIP= 108.160.141.216	
	MsgServerPort=8100
	msfs=http:// 108.160.141.216：8700/
	discovery=http:// 108.160.141.216/api/discover
	
**msg_server:**
	
	ListenIP= 108.160.141.216
	ListenPort=8000

	ConcurrentDBConnCnt=2
	DBServerIP1= 108.160.141.216
	DBServerPort1=10600
	DBServerIP2= 108.160.141.216
	DBServerPort2=10600

	LoginServerIP1= 108.160.141.216
	LoginServerPort1=8100

	RouteServerIP1= 108.160.141.216
	RouteServerPort1=8400
	
	PushServerIP1= 108.160.141.216
	PushServerPort1=8500

	FileServerIP1= 108.160.141.216
	FileServerPort1=8600

	IpAddr1= 108.160.141.216 	
	IpAddr2= 108.160.141.216		
	MaxConnCnt=100000
	
**route_server:**

	ListenIP= 108.160.141.216			
	ListenMsgPort=8400
	
**msfs_server:**

	ListenIP= 108.160.141.216		
	ListenPort=8600
	BaseDir=./tmp
	FileCnt=0
	FilesPerDir=30000
	GetThreadCount=32
	PostThreadCount=1
	
**file_server:**
	
	Address= 108.160.141.216	
	ListenPort=8500			
	TaskTimeout=60        
	
**db_proxy:**
	
	ListenIP= 108.160.141.216	
	ListenPort=10600
	ThreadNum=48		# double the number of CPU core
	MsfsSite= 108.160.141.216	

	#configure for mysql
	DBInstances=teamtalk_master,teamtalk_slave
	#teamtalk_master
	teamtalk_master_host= 108.160.141.216
	teamtalk_master_port=3306
	teamtalk_master_dbname=teamtalk
	teamtalk_master_username=root
	teamtalk_master_password=12345
	teamtalk_master_maxconncnt=16

	#teamtalk_slave
	teamtalk_slave_host= 108.160.141.216
	teamtalk_slave_port=3306
	teamtalk_slave_dbname=teamtalk
	teamtalk_slave_username=root
	teamtalk_slave_password=12345
	teamtalk_slave_maxconncnt=16


	#configure for unread
	CacheInstances=unread,group_set,token,sync,group_member
	#未读消息计数器的redis
	unread_host= 108.160.141.216
	unread_port=6379
	unread_db=1
	unread_maxconncnt=16

	#群组设置redis
	group_set_host= 108.160.141.216
	group_set_port=6379
	group_set_db=2
	group_set_maxconncnt=16

	#同步控制
	sync_host= 108.160.141.216
	sync_port=6379
	sync_db=3
	sync_maxconncnt=1

	#deviceToken redis
	token_host= 108.160.141.216
	token_port=6379
	token_db=4
	token_maxconncnt=16

	#GroupMember
	group_member_host= 108.160.141.216
	group_member_port=6379
	group_member_db=5
	group_member_maxconncnt=48

**http_msg_server:**

	ListenIP= 108.160.141.216
	ListenPort=8400

	ConcurrentDBConnCnt=4
	DBServerIP1= 108.160.141.216
	DBServerPort1=10600
	DBServerIP2= 108.160.141.216
	DBServerPort2=10600

	RouteServerIP1= 108.160.141.216
	RouteServerPort1=8200
	#RouteServerIP2=localhost	
	#RouteServerPort2=8201

**push_server:**
	
	ListenIP= 108.160.141.216
	ListenPort=8500

	CertPath=apns-dev-cert.pem
	KeyPath=apns-dev-key.pem
	KeyPassword=tt@mogujie

	#SandBox
	#1: sandbox 0: production
	SandBox=0	

###2.公网ip
	安装的机器为多网卡，包含内网网卡和公网网卡
	内网ip为： 108.160.141.216
	公网ip为122.222.222.222


**login_server:**

	ClientListenIP=108.160.141.216		
	ClientPort=8008
	HttpListenIP=108.160.141.216	
	HttpPort=8080
	MsgServerListenIP= 108.160.141.216	
	MsgServerPort=8100
	msfs=http://108.160.141.216	:8700/
	discovery=http://108.160.141.216/api/discover
	
**msg_server:**
	
	ListenIP=122.222.222.222
	ListenPort=8000

	ConcurrentDBConnCnt=2
	DBServerIP1= 108.160.141.216
	DBServerPort1=10600
	DBServerIP2= 108.160.141.216
	DBServerPort2=10600

	LoginServerIP1= 108.160.141.216
	LoginServerPort1=8100

	RouteServerIP1= 108.160.141.216
	RouteServerPort1=8400
	
	PushServerIP1= 108.160.141.216
	PushServerPort1=8500

	FileServerIP1= 108.160.141.216
	FileServerPort1=8600

	IpAddr1=108.160.141.216	
	IpAddr2=108.160.141.216	
	MaxConnCnt=100000
	
**route_server:**

	ListenIP= 108.160.141.216			
	ListenMsgPort=8400
	
**msfs_server:**

	ListenIP= 108.160.141.216;108.160.141.216		
	ListenPort=8600
	BaseDir=./tmp
	FileCnt=0
	FilesPerDir=30000
	GetThreadCount=32
	PostThreadCount=1
	
**file_server:**
	
	Address=108.160.141.216
	ListenPort=8500			
	TaskTimeout=60        
	
**db_proxy:**
	
	ListenIP= 108.160.141.216	
	ListenPort=10600
	ThreadNum=48		# double the number of CPU core
	MsfsSite= 108.160.141.216	

	#configure for mysql
	DBInstances=teamtalk_master,teamtalk_slave
	#teamtalk_master
	teamtalk_master_host= 108.160.141.216
	teamtalk_master_port=3306
	teamtalk_master_dbname=teamtalk
	teamtalk_master_username=root
	teamtalk_master_password=12345
	teamtalk_master_maxconncnt=16

	#teamtalk_slave
	teamtalk_slave_host= 108.160.141.216
	teamtalk_slave_port=3306
	teamtalk_slave_dbname=teamtalk
	teamtalk_slave_username=root
	teamtalk_slave_password=12345
	teamtalk_slave_maxconncnt=16


	#configure for unread
	CacheInstances=unread,group_set,token,sync,group_member
	#未读消息计数器的redis
	unread_host= 108.160.141.216
	unread_port=6379
	unread_db=1
	unread_maxconncnt=16

	#群组设置redis
	group_set_host= 108.160.141.216
	group_set_port=6379
	group_set_db=2
	group_set_maxconncnt=16

	#同步控制
	sync_host= 108.160.141.216
	sync_port=6379
	sync_db=3
	sync_maxconncnt=1

	#deviceToken redis
	token_host= 108.160.141.216
	token_port=6379
	token_db=4
	token_maxconncnt=16

	#GroupMember
	group_member_host= 108.160.141.216
	group_member_port=6370
	group_member_db=5
	group_member_maxconncnt=48

**http_msg_server:**

	ListenIP= 108.160.141.216
	ListenPort=8400

	ConcurrentDBConnCnt=4
	DBServerIP1= 108.160.141.216
	DBServerPort1=10600
	DBServerIP2= 108.160.141.216
	DBServerPort2=10600

	RouteServerIP1= 108.160.141.216
	RouteServerPort1=8200
	#RouteServerIP2=localhost	
	#RouteServerPort2=8201

**push_server:**
	
	ListenIP= 108.160.141.216
	ListenPort=8500

	CertPath=apns-dev-cert.pem
	KeyPath=apns-dev-key.pem
	KeyPassword=tt@mogujie

	#SandBox
	#1: sandbox 0: production
	SandBox=0	


###3.公网ip，路由器映射
######此种情况请确保在内网下可以访问路由器映射的外网ip

	安装的机器为单网卡，外网由路由器映射
	内网ip为:  108.160.141.216
	路由器映射的公网ip为: 108.160.141.216
**login_server:**

	ClientListenIP= 108.160.141.216		
	ClientPort=8008
	HttpListenIP= 108.160.141.216
	HttpPort=8080
	MsgServerListenIP= 108.160.141.216	
	MsgServerPort=8100
	msfs=http://108.160.141.216	:8700/
	discovery=http://108.160.141.216/api/discover
	
**msg_server:**
	
	ListenIP= 108.160.141.216
	ListenPort=8000

	ConcurrentDBConnCnt=2
	DBServerIP1= 108.160.141.216
	DBServerPort1=10600
	DBServerIP2= 108.160.141.216
	DBServerPort2=10600

	LoginServerIP1= 108.160.141.216
	LoginServerPort1=8100

	RouteServerIP1= 108.160.141.216
	RouteServerPort1=8400
	
	PushServerIP1= 108.160.141.216
	PushServerPort1=8500

	FileServerIP1= 108.160.141.216
	FileServerPort1=8600

	IpAddr1=108.160.141.216	
	IpAddr2=108.160.141.216		
	MaxConnCnt=100000
	
**route_server:**

	ListenIP= 108.160.141.216			
	ListenMsgPort=8400
	
**msfs_server:**

	ListenIP= 108.160.141.216		
	ListenPort=8600
	BaseDir=./tmp
	FileCnt=0
	FilesPerDir=30000
	GetThreadCount=32
	PostThreadCount=1
	
**file_server:**
	
	Address=108.160.141.216	
	ListenPort=8500			
	TaskTimeout=60        
	
**db_proxy:**
	
	ListenIP= 108.160.141.216	
	ListenPort=10600
	ThreadNum=48		# double the number of CPU core
	MsfsSite= 108.160.141.216	

	#configure for mysql
	DBInstances=teamtalk_master,teamtalk_slave
	#teamtalk_master
	teamtalk_master_host= 108.160.141.216
	teamtalk_master_port=3306
	teamtalk_master_dbname=teamtalk
	teamtalk_master_username=root
	teamtalk_master_password=12345
	teamtalk_master_maxconncnt=16

	#teamtalk_slave
	teamtalk_slave_host= 108.160.141.216
	teamtalk_slave_port=3306
	teamtalk_slave_dbname=teamtalk
	teamtalk_slave_username=root
	teamtalk_slave_password=12345
	teamtalk_slave_maxconncnt=16


	#configure for unread
	CacheInstances=unread,group_set,token,sync,group_member
	#未读消息计数器的redis
	unread_host= 108.160.141.216
	unread_port=6379
	unread_db=1
	unread_maxconncnt=16

	#群组设置redis
	group_set_host= 108.160.141.216
	group_set_port=6379
	group_set_db=2
	group_set_maxconncnt=16

	#同步控制
	sync_host= 108.160.141.216
	sync_port=6379
	sync_db=3
	sync_maxconncnt=1

	#deviceToken redis
	token_host= 108.160.141.216
	token_port=6379
	token_db=4
	token_maxconncnt=16

	#GroupMember
	group_member_host= 108.160.141.216
	group_member_port=6379
	group_member_db=5
	group_member_maxconncnt=48

**http_msg_server:**

	ListenIP= 108.160.141.216
	ListenPort=8400

	ConcurrentDBConnCnt=4
	DBServerIP1= 108.160.141.216
	DBServerPort1=10600
	DBServerIP2= 108.160.141.216
	DBServerPort2=10600

	RouteServerIP1= 108.160.141.216
	RouteServerPort1=8200
	#RouteServerIP2=localhost	
	#RouteServerPort2=8201

**push_server:**
	
	ListenIP= 108.160.141.216
	ListenPort=8500

	CertPath=apns-dev-cert.pem
	KeyPath=apns-dev-key.pem
	KeyPassword=tt@mogujie

	#SandBox
	#1: sandbox 0: production
	SandBox=0	
	
	