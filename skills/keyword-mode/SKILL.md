# 关键词搜索模式 (Keyword Mode)

## 适用场景

通过搜索特定关键词、标签或用户来发现帖子并进行评论。

支持三种搜索格式：
- `@username` — 搜索用户主页
- `#hashtag` — 搜索话题标签
- `keyword` — 搜索关键词

## 完整参数表

| 参数 | 类型 | 必需 | 默认值 | 说明 |
|------|------|------|--------|------|
| `mode` | String | 是 | - | 固定值：`"keyword"` |
| `accounts` | Array | 是 | - | 账号数组，每个包含 name、serialNumber |
| `searchQueries` | Array | 是 | - | 搜索关键词数组 |
| `postsPerQuery` | Number | 否 | 3 | 每个关键词评论的帖子数 |
| `postSelectionMode` | String | 否 | "random" | 帖子选择策略 |
| `comments` | Array | 否 | [] | 固定评论内容列表 |
| `maxComments` | Number | 否 | 50 | 最大评论数上限 |
| `waitTime` | Object | 否 | {min:10, max:30} | 评论间等待时间（秒） |

## curl 示例

```bash
curl -X POST http://localhost:3000/api/start \
  -H "Content-Type: application/json" \
  -d '{
    "mode": "keyword",
    "accounts": [{"name": "账号1", "serialNumber": "SERIAL_001"}],
    "searchQueries": ["#ootd", "fashion"],
    "postsPerQuery": 5,
    "comments": ["Great!", "Nice!"],
    "maxComments": 50
  }'
```
