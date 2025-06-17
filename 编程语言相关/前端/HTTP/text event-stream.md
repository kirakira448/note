## 1. 什么是 `text/event-stream`？

- `text/event-stream` 是 SSE（Server-Sent Events）协议的 MIME 类型。
- SSE 是一种单向通信协议，允许服务器向客户端持续推送事件（数据）。
- 客户端使用 `EventSource` API 与服务器建立连接。

---

## 2. SSE 特点

- 单向通信（服务器 ➝ 客户端）
- 基于 HTTP 协议（不需要升级协议）
- 支持自动重连
- 浏览器原生支持（兼容性好）
- 比 WebSocket 简单，适合数据通知、进度推送、日志流等场景

---

## 3. SSE 消息格式

每条 SSE 消息格式如下：
```yaml
data: 消息内容（字符串或 JSON）  
event: 可选的自定义事件名  
id: 可选的事件 ID  
retry: 可选，重连时间（毫秒）
```
一个完整消息以空行 `\n\n` 结束：

```text
data: Hello world!

data: {"progress": 90}

event: customEvent
data: Finished
```

## 4. FastAPI 实现下载进度推送（SSE 示例）

### ✅ Python 服务端代码（FastAPI）
```python
from fastapi import FastAPI, BackgroundTasks
from fastapi.responses import StreamingResponse
import time

app = FastAPI()

# 用于记录进度
progress = {
    "value": 0,
    "done": False
}

# 模拟下载任务
def fake_download_task():
    global progress
    for i in range(1, 101):
        time.sleep(0.1)
        progress["value"] = i
    progress["done"] = True

# 启动下载任务
@app.post("/download")
def start_download(background_tasks: BackgroundTasks):
    global progress
    progress = {"value": 0, "done": False}
    background_tasks.add_task(fake_download_task)
    return {"message": "Download started"}

# SSE 推送进度
@app.get("/progress")
def progress_stream():
    def event_stream():
        while not progress["done"]:
            yield f"data: {progress['value']}\n\n"
            time.sleep(0.5)
        yield f"data: DONE\n\n"
    return StreamingResponse(event_stream(), media_type="text/event-stream")

```

## 5. HTML 客户端示例

```html
<button onclick="startDownload()">开始下载</button>
<div id="progress">等待下载...</div>

<script>
function startDownload() {
  fetch("/download", { method: "POST" });

  const source = new EventSource("/progress");
  source.onmessage = function(event) {
    if (event.data === "DONE") {
      document.getElementById("progress").innerText = "下载完成";
      source.close();
    } else {
      document.getElementById("progress").innerText = "下载进度: " + event.data + "%";
    }
  };
}
</script>

```

## 6. 注意事项

- SSE 是单向通信，如需双向通信可使用 WebSocket。
    
- 如果部署在 Nginx 之后，需要开启：
    
    - `proxy_buffering off;`
        
    - 设置合适的 `keepalive` 超时时间
        
- Python 中若需要多用户支持，应考虑使用 Redis 等持久存储方案来跟踪用户进度。

## 7. 适用场景

- 实时日志输出（如 CI 构建日志）
    
- 下载 / 上传进度推送
    
- 后台任务执行状态通知
    
- 实时消息通知（如公告）

## 8. 与 WebSocket 区别

|特性|SSE|WebSocket|
|---|---|---|
|协议|HTTP|自定义协议（需升级）|
|连接方向|单向（服务端 ➝ 客户端）|双向|
|简单性|非常简单，浏览器原生支持|更复杂|
|适用场景|通知/日志/进度/推送|聊天/游戏/数据同步等|