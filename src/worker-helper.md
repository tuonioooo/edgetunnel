# worker.js 说明文档


| **方法名称**           | **作用描述**                                                                                   |
|------------------------|-----------------------------------------------------------------------------------------------|
| **fetch**              | 处理 Cloudflare 的 HTTP 和 WebSocket 请求。                                                   |
|                        | - `/`：返回请求的 Cloudflare 元数据。                                                         |
|                        | - `/UUID`：生成 VLESS 配置文件。                                                              |
|                        | - 其他路径：返回 404。                                                                        |
|                        | 对 WebSocket 请求调用 `vlessOverWSHandler` 方法进行处理。                                      |
|                        | `env` 参数是设置 Workers 中配置的动态变量。                                                   |
| **vlessOverWSHandler** | 用于处理 WebSocket 请求，并将其转换为远程服务器的 TCP/UDP 连接。                                |
| **handleTCPOutBound**  | 建立与远程服务器的 TCP 连接，并将数据从 WebSocket 转发至远程服务器。                            |
| **makeReadableWebSocketStream** | 将 WebSocket 消息流转换为可读流，供管道传输使用。                                      |
| **processVlessHeader** | 解析 VLESS 协议头部数据，并返回解析结果。                                                      |
| **isValidUUID**        | 验证 UUID 的格式。                                                                            |
| **remoteSocketToWS**   | 用于将远程 Socket 的数据转发到 WebSocket，并管理数据流动、错误处理及可能的重试逻辑。            |
|                        | - **数据转发**：将从远程服务器读取的数据通过 WebSocket 发送到客户端。                          |
|                        | - **流量管理**：支持对接收到的数据块进行初步处理（例如添加 VLESS 响应头）。                     |
|                        | - **错误处理**：捕获异常并在需要时关闭 WebSocket。                                              |
|                        | - **连接重试**：当远程 Socket 没有数据传入时尝试重新建立连接（如果提供 `retry` 函数）。        |
| **handleUDPOutBound**  | 专门处理 UDP 出站连接，支持将 UDP 数据通过 WebSocket 转发到远程服务器，并返回响应数据。          |
| **base64ToArrayBuffer**| 将 Base64 转换成缓存数组。                                                                     |
| **safeCloseWebSocket** | 安全地关闭 WebSocket。                                                                         |
| **getVLESSConfig**     | 返回 VLESS 的基本配置信息，例如 V2Ray 链接和订阅链接。                                          |


