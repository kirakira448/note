
[官方文档](https://docs.influxdata.com/influxdb/v2/install/?t=Linux)

## [Download and install InfluxDB v2](https://docs.influxdata.com/influxdb/v2/install/?t=Linux#download-and-install-influxdb-v2)
### 1. 根据操作系统选择`key-pair`


_Before running the installation steps, substitute the InfluxData key-pair compatible with your OS version:_

For newer releases (for example, Ubuntu 20.04 LTS and newer, Debian Buster and newer) that support subkey verification:

- Private key file: [`influxdata-archive.key`](https://repos.influxdata.com/influxdata-archive.key)
- Public key: `943666881a1b8d9b849b74caebf02d3465d6beb716510d86a39f6c8e8dac7515`

For older versions (for example, CentOS/RHEL 7, Ubuntu 18.04 LTS, or Debian Stretch) that don’t support subkeys for verification:

- Private key file: [`influxdata-archive_compat.key`](https://repos.influxdata.com/influxdata-archive_compat.key)
- Public key: `393e8779c89ac8d958f81f942f9ad7fb82a25e133faddaf92e15b16e6ac9ce4c`

### 2. 初始化`key-pair`

注意这里使用第一步选择的key-pair
```bash
# Ubuntu and Debian
curl --silent --location -O https://repos.influxdata.com/influxdata-archive.key \
&& echo "943666881a1b8d9b849b74caebf02d3465d6beb716510d86a39f6c8e8dac7515  influxdata-archive.key" \
| sha256sum --check - \
&& cat influxdata-archive.key | gpg --dearmor \
| sudo tee /etc/apt/trusted.gpg.d/influxdata-archive.gpg > /dev/null \
&& echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive.gpg] https://repos.influxdata.com/debian stable main' \
| sudo tee /etc/apt/sources.list.d/influxdata.list
```

执行成功后出现如下信息
```text
influxdata-archive.key: OK
deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive.gpg] https://repos.influxdata.com/debian stable main
```


### 3. 安装InfluxDB

```bash
sudo apt-get update && sudo apt-get install influxdb2
```


### 4. 启动服务

```bash
sudo service influxdb start
```

查看运行状态
```bash
systemctl status influxdb
```

查看监听端口
```bash
sudo lsof -i -n -P | grep influxd
```
### 5. 配置项

