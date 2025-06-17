# 1.以管理员权限打开VSCODE
# 2.查看当前状态
```bash
Get-ExecutionPolicy
```
output:
Restricted

# 3.修改权限
```bash
set-ExecutionPolicy RemoteSigned
```
输入`y`选项

# 4.再次查看状态
若成功，显示`RemoteSigned`

# 5.重启VSCODE

