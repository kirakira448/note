
## 安装

```bash
pip install flask-migrate
```

## 基本命令

### 创建迁移仓库

这个命令会创建migrations文件夹，所有迁移文件都放在里面。
只用执行一次
```
flask db init
```

### 生成脚本文件
```
flask db migrate
```

### 更新数据库

^5a1337

```
flask db upgrade
```

### 返回以前的版本
```
flask db downgrade version_
```


## 使用方法

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy


app = Flask(__name__)


# 数据库的变量
HOST = '192.168.30.151' # 127.0.0.1/localhost
PORT = 3306
DATA_BASE = 'flask_db'
USER = 'root'
PWD = '123'
DB_URI = f'mysql+pymysql://{USER}:{PWD}@{HOST}:{PORT}/{DATA_BASE}'
# mysql+pymysql://root:123@192.168.30.151/flask_db


app.config['SQLALCHEMY_DATABASE_URI'] = DB_URI
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False


db = SQLAlchemy(app)


# 创建模型类
class User(db.Model):
  __tablename__ = 't_user'
  id = db.Column(db.Integer,primary_key = True,autoincrement = True)
  name = db.Column(db.String(32))
  age = db.Column(db.Integer)


  def __repr__(self):
    return f'<User id={self.id}  name={self.name}>'


from flask_migrate import Migrate


Migrate(app,db)

```

当模型类发生更新时，依次执行[[#^3ceafb|生成脚本文件]]，[[#^5a1337| 更新数据库]]

