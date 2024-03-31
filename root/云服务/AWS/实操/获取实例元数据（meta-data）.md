
(已连接实例)使用命令
```shell
curl http://169.254.169.254/latest/meta-data
```

返回元数据名称
```text
ami-id
ami-launch-index
ami-manifest-path
block-device-mapping/
events/
hostname
identity-credentials/
instance-action
instance-id
instance-life-cycle
instance-type
local-hostname
local-ipv4
mac
managed-ssh-keys/
metrics/
network/
placement/
profile
public-hostname
public-ipv4
public-keys/
reservation-id
security-groups
services/
```

例如：获取实例本地ipv4
```shell
curl http://169.254.169.254/latest/meta-data/local-ipv4
```

返回值：
```text
172.31.0.156[ec2-user@ip-172-31-0-156 ~]$ 
```

