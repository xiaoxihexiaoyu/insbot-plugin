# 养号模式 (Nurture Mode)

## 适用场景

模拟真实用户行为来"养号"，降低风控风险。

## 完整参数表

| 参数 | 类型 | 必需 | 默认值 | 说明 |
|------|------|------|--------|------|
| `mode` | String | 是 | - | 固定值：`"nurture"` |
| `accounts` | Array | 是 | - | 账号数组 |
| `nurtureTopics` | Array | 是 | - | 搜索主题数组 |
| `nurturePostsPerTopic` | Number | 否 | 5 | 每主题处理帖子数 |
| `nurtureLikeRate` | Number | 否 | 70 | 点赞概率（%） |
| `nurtureCommentRate` | Number | 否 | 20 | 评论概率（%） |
| `nurtureViewMin` | Number | 否 | 3 | 最小浏览时长（秒） |
| `nurtureViewMax` | Number | 否 | 8 | 最大浏览时长（秒） |
| `commentsList` | Array | 否 | [] | 评论内容列表 |

## curl 示例

```bash
curl -X POST http://localhost:3000/api/start \
  -H "Content-Type: application/json" \
  -d '{
    "mode": "nurture",
    "accounts": [{"name": "账号1", "serialNumber": "SERIAL_001"}],
    "nurtureTopics": ["#fashion", "#style"],
    "nurtureLikeRate": 70,
    "nurtureCommentRate": 20,
    "commentsList": ["Nice!", "Great!"]
  }'
```
