# URL 批量发送模式 (URL Mode)

## 适用场景

有预先准备好的帖子 URL 列表，批量访问并评论。

## 完整参数表

| 参数 | 类型 | 必需 | 默认值 | 说明 |
|------|------|------|--------|------|
| `mode` | String | 是 | - | 固定值：`"url"` |
| `accounts` | Array | 是 | - | 账号数组，可包含 urls |
| `useAccountUrls` | Boolean | 是 | - | 是否使用账号独立 URL |
| `urlFile` | String | 否 | - | URL 文件路径（全局模式） |
| `comments` | Array | 否 | [] | 固定评论内容列表 |
| `maxComments` | Number | 否 | 50 | 最大评论数上限 |
| `commentsPerAccount` | Number | 否 | 5 | 每账号评论数后切换 |
| `waitTime` | Object | 否 | {min:10, max:30} | 评论间等待时间（秒） |

## curl 示例

### 账号独立 URL（推荐）

```bash
curl -X POST http://localhost:3000/api/start \
  -H "Content-Type: application/json" \
  -d '{
    "mode": "url",
    "accounts": [
      {
        "name": "账号1",
        "serialNumber": "SERIAL_001",
        "urls": ["https://www.instagram.com/p/ABC123/"]
      }
    ],
    "useAccountUrls": true,
    "comments": ["Nice!"],
    "maxComments": 30
  }'
```
