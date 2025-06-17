## 1. 安装

### 1.1 下载 Protobuf 编译器
1. 访问 Protocol Buffers GitHub Releases 页面。
2. 在页面中找到最新版本（例如 v24.x.x），并下载适用于 Windows 的预编译二进制文件。文件名通常是类似 `protoc-<version>-win64.zip`。
3. 解压下载的 `.zip` 文件。你会看到一个 bin 文件夹，里面包含 `protoc.exe`，以及一个 `include` 文件夹，里面包含 `.proto` 的标准定义。

### 1.2 配置环境变量

1. 打开你的电脑的 `环境变量` 设置。
2. 在 `系统变量` 中找到 `Path`，并编辑。
3. 在 `Path` 变量中添加 `protoc.exe` 的路径。例如：

```bash
C:\path\to\protoc\bin
```

### 1.3 安装 Python 的 Protobuf 库

```bash
pip install protobuf
```

## 2. 使用

### 2.1 编写 `.proto` 文件

```proto
syntax = "proto3";

message Person {
  string name = 1;
  int32 id = 2;
  string email = 3;
}
```

### 2.2 编译 `.proto` 文件  

```bash
protoc --python_out=. person.proto
```

### 2.3 使用生成的 Python 代码

```python
import person_pb2

# 创建一个 Person 对象
person = person_pb2.Person()
person.name = "Alice"
person.id = 1234
person.email = "alice@example.com"

# 序列化为二进制格式
serialized_person = person.SerializeToString()

# 反序列化回对象
person2 = person_pb2.Person()
person2.ParseFromString(serialized_person)

# 打印对象内容
print(f"Name: {person2.name}, ID: {person2.id}, Email: {person2.email}")
```



