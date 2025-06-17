
一般flask这样指定host:port
```python
if __name__ == '__main__':
    app.run(debug=True,host='0.0.0.0', port=8080)
```

PyCharm中不能直接像这样指定，需要添加运行参数来指定

run-Edit-Configuration 中,找到Additinal options栏 ：手动写入 --host=x.x.x.x --port=xxxx。

1. 选择 `Edit...`
![[Snipaste_2024-02-07_23-13-56.png]]

2. Additinal options栏输入参数
![[Snipaste_2024-02-07_23-16-12.png]]