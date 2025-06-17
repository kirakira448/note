
有些教程使用linux环境的docker进行配置，有时会设置一些环境参数，但是在windows下无效。

## 解决方法

进入Windows下的docker的Linux环境中就可以用了

```bash
wsl -d docker-desktop
```


## 案例

### 问题
配置 Elasticsearch 时，需要执行如下操作

- 修改虚拟内存区域大小，否则会因为过小而无法启动:

```bash
sysctl -w vm.max_map_count=262144
```

但是在windows的cmd或powershell下无法直接使用

### 正确做法：

1. 进入docker-desktop
```bash
wsl -d docker-desktop
```

2. 执行命令
```bash
sysctl -w vm.max_map_count=262144
```