---
layout: post
title: " Flask Link MySQL"
date: 2020-03-25 20:30:00 + 0800
categories：technology
tags: [flask]
img: https://ooo.0o0.ooo/2017/05/27/5929398cad637.jpg
---

# Flask Link MySQL

## 准备配置文件

### 根目录下创建config.py

```python

# config.py

# 配置 sqlalchemy  "数据库+数据库驱动://数据库用户名:密码@主机地址:端口/数据库?编码"
SQLALCHEMY_DATABASE_URI = "mysql+pymysql://root:123456@114.116.4.196:3306/learnflaskdb?charset=UTF8MB4"

SQLALCHEMY_TRACK_MODIFICATIONS = True

SECRET_KEY = 'Fianna'
```

### 根目录下创建db.py

```python
# db.py

from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()
```

## 在启动文件中设置

### 引入包

```python
from db import db
```

### 加载配置信息

```python
# 加载配置信息，其中有数据库的配置信息，包含在SQLALCHEMY_DATABASE_URI中
app.config.from_object('config')
```

### 初始化db

```python
# 初始化db,并创建models中定义的表格
# 添加这一句，否则会报数据库找不到application和context错误
with app.app_context():
    # 初始化db
    db.init_app(app)
    # 创建所有未创建的table
    db.create_all()
```

## 新建一个models包

![截屏2020-03-24下午10.05.29](https://tva1.sinaimg.cn/large/00831rSTly1gd5dbtw9uhj30fm02e74a.jpg)

![截屏2020-03-24下午10.06.07](https://tva1.sinaimg.cn/large/00831rSTly1gd5dckj1voj30g60cqdge.jpg)

### 在包里创建一个Py文件

> 内部为一个类
>
> * 定义是数据类型
> * 用数据类型创建数据表
> * 提供数据表的操作方法

### Models.py

* Import package

  ```python
  from db import db
  from sqlalchemy import and_
  ```

* Create model and table

  ```python
  class User(db.Model):

      # （设置表名）
      __tablename__ = 'user_list'

      # （设置主键）
      id = db.Column(db.Integer, primary_key=True)

      username = db.Column(db.String(255),)

      password = db.Column(db.String(255),)

  # 返回一个可以用来表示对象的可打印字符串：（相当于java的toString）
      def __repr__(self):
          return '<User 用户名：%r 密码：%r>' % (self.username, self.password)# 操作数据库
  ```

* Functions

  ```python
  # 增
  def add_object(user):
      db.session.add(user)
      db.session.commit()
      print("添加 % r 完成" % user.__repr__)

  # 查 （用到and的时候需要导入库from sqlalchemy import and_）
  def query_object(user, query_condition_u, query_condition_p):
      result = user.query.filter(and_(user.username == query_condition_u, user.password == query_condition_p))
      print("查询 % r 完成" % user.__repr__)
      return result

  # 删
  def delete_object(user):
      result = user.query.filter(user.username == '11111').all()
      db.session.delete(result)
      db.session.commit()

  #改
  def update_object(user):
      result = user.query.filter(user.username == '111111').all()
      result.title = 'success2018'
  ```



