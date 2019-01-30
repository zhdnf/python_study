sqlalchemy

---
## 一、基本概念

采用orm技术：Object-Relational Mapping， 把关系数据库的表结构映射到对象上。可以兼容多种数据库（mysql，sqlite，sqlserver等等）

---
## 二、模块内容
1. 模块版本查看(Version Check)
	```
	import sqlalchemy
	sqlalchemy.__version
	```
2. 连接数据库(Connecting)
	```
	from sqlalchemy import create_engine
	engine = create_engine('数据库类型+数据库驱动://账号:密码@地址:端口/数据库名')
	#例如mysql的数据库+pymysql的python Mysql驱动
	engine = create_engine('mysql+pymysql://root:passwd@localhost:3306/test')
	```
3. 声明映射关系(Declare a Mapping)
	```
	from sqlalchemy.ext.declarative import declarative.base
	from sqlalchemy import Column,Integer,String
	Base = declarative_base()
	```
4. 数据库相关操作   
	```
	#创建表
	class User(Base)
		__tablename__ = 'users'
		id = Column(Integer, primary_key=True)
		name = Column(String)
		password = Column(String)
		def __repr__(self)：
			return "<User(name='%s',password='%s')>"%(self.name, self.password)
	#表结构
	User.__table__
	#绑定映射
	Base.metadata.create_all(engine)
	#创建表数据
	ed_user = User(name = 'ed', password= '123456')
	#查看数据
	ed_user.name
	ed_user.password
	#id为None
	ed_user.id
    ```
5. 会话（Creating a Session）
	```
	from sqlalchemy.orm import sessionmaker
	#绑定会话
	Session = sessionmaker(bind=engine)
	session = Session()
	#添加一条数据
	session.add(ed_user)
	#查询
	our_user = session.query(User).filter_by(name='ed').first()
	our_user
	#添加多条数据
	session.add_all([
		User(name='wendy',password='123456'),
		User(name='wendy',password='123456')
	])
	#修改数据（修改对象即可）
	ed_user.password = '654321'
	#以前的session
	session.dirty
	#现在的session
	session.new
	#提交session后数据库才会添加数据
	session.commit()
	#id号存在
	ed_user.id
	```
6. 其他内容

	数据库回滚，sql语句等的详细细节请看官方帮助文档
	
---
## 三、帮助文档
	1.1版本:https://docs.sqlalchemy.org/en/rel_1_1/
	1.2版本:https://docs.sqlalchemy.org/en/latest/
	
	
	
	
	
	
	
