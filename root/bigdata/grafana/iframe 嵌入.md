

### 1. 修改配置文件
```bash
sudo nano /etc/grafana/grafana.ini
```

需要修改两个地方
1. 允许匿名访问

原始状态：
```ini
[auth.anonymous] 
# enable anonymous access 
;enabled = false
```

修改后：
```ini
[auth.anonymous] 
# enable anonymous access 
enabled = true
```

>注意:
>需要把`;`删掉


2. #### 允许被iFrame嵌入

原始状态：
```ini
# set to true if you want to allow browsers to render Grafana in a <frame>, <iframe>, <embed> or <object>. default is false.
;allow_embedding = false
```

修改后：
```ini
# set to true if you want to allow browsers to render Grafana in a <frame>, <iframe>, <embed> or <object>. default is false.
allow_embedding = true
```

### 2. 重启服务
```bash
systemctl restart grafana-server
```

### 3. 查看效果

使用`Share`->`Embed`生成`<iframe/>`，嵌入到网页中
现在可以正常访问了