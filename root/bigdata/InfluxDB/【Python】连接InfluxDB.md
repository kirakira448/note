
### 1. 安装工具包

```bash
pip install influxdb-client
```

### 2. 配置token

influxdb启动后会生成一个token，可以进入webUI界面找到

![[Pasted image 20241016094506.png]]

在项目目录下创建`.env`文件，将token写入
```env
INFLUXDB_TOKEN=9YUzFZZQAWLludrFI1_ZBZs5_j7F8UDtl2ZiZQUH-F8cgopECGXrOPqgXSDSSf-nwXdQeRstXmudGD-xdFrAdA==
```

在项目启动时加载环境变量
```python
from dotenv import load_dotenv
import os

# 加载.env中的环境变量
load_dotenv()
# 如果要指定 .env 文件路径
# load_dotenv(dotenv_path='path/to/your/.env')
print('INFLUXDB_TOKEN:', os.getenv('INFLUXDB_TOKEN'))
```

### 3. 连接

```python 
import influxdb_client, os, time


token = os.environ.get("INFLUXDB_TOKEN")
org = "hoso"
url = "http://10.177.1.130:8086"

client = influxdb_client.InfluxDBClient(url=url, token=token, org=org)
```