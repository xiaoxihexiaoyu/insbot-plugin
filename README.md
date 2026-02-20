# InstaBot Claude Code 插件

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude_Code-Plugin-blue)](https://claude.ai/claude-code)
[![Version](https://img.shields.io/badge/version-1.0.0-green)](CHANGELOG.md)

[InstaBot](https://github.com/your-repo/insta-bot) 的 Claude Code 插件，通过自然语言控制 Instagram 自动化评论机器人。

## 功能

- 🔍 **关键词搜索模式**：搜索标签、用户、关键词，自动评论
- 📋 **URL 批量模式**：批量处理预设的帖子 URL 列表
- 🌱 **养号模式**：模拟真实用户行为，降低风控风险

## 安装

### 方式一：项目级安装（推荐）

```bash
# 在你的项目目录下
claude --plugin-dir ./insbot-plugin
```

### 方式二：用户级安装

```bash
# 复制到用户级插件目录
cp -r insbot-plugin ~/.claude/plugins/insbot
```

## 前置要求

1. **AdsPower** 正在运行
   - 下载：https://www.adspower.net/

2. **启动 API 服务器**
   ```bash
   cd insta_bot_ui
   npm install
   node api/server.js
   ```

3. **配置浏览器账号**
   - 在 AdsPower 中创建浏览器配置
   - 记录每个浏览器的序列号（Serial Number）

## 使用

### 主命令（自然语言）

```bash
# 查看状态
/insbot:insbot 查看机器人状态

# 启动关键词搜索
/insbot:insbot 用账号5搜索 #ootd，评论"Great!"

# 启动 URL 批量
/insbot:insbot 用 urls.csv 文件批量发送评论

# 启动养号模式
/insbot:insbot 开启养号模式，浏览 #fashion 话题

# 停止任务
/insbot:insbot 停止当前任务
```

### 快捷命令

```bash
# 关键词搜索模式
/insbot:keyword 账号1 搜索 #ootd
/insbot:keyword 账号5 搜索 @competitor1 AI评论

# URL 批量模式
/insbot:url 账号1 文件 urls.csv
/insbot:url 账号1,账号2 账号配置 AI评论

# 养号模式
/insbot:nurture 账号1 浏览 #fashion 标准
/insbot:nurture 账号1,账号2,账号3 浏览 #fitness 轻量
```

## 命令参考

| 命令 | 说明 |
|------|------|
| `/insbot:insbot` | 主入口，自然语言控制 |
| `/insbot:keyword` | 关键词搜索模式快捷入口 |
| `/insbot:url` | URL 批量模式快捷入口 |
| `/insbot:nurture` | 养号模式快捷入口 |

## API 端点

插件通过 HTTP API 与 InstaBot 通信：

| 端点 | 方法 | 说明 |
|------|------|------|
| `/api/health` | GET | 健康检查 |
| `/api/start` | POST | 启动任务 |
| `/api/status` | GET | 查询状态 |
| `/api/stop` | POST | 停止任务 |

示例：

```bash
# 健康检查
curl http://localhost:3000/api/health

# 查询状态
curl http://localhost:3000/api/status
```

## 配置示例

### 关键词搜索

```json
{
  "mode": "keyword",
  "accounts": [
    {"name": "账号1", "serialNumber": "BROWSER_SERIAL_001"}
  ],
  "searchQueries": ["#ootd", "fashion"],
  "postsPerQuery": 5,
  "comments": ["Great!", "Nice!", "Love it!"],
  "maxComments": 50,
  "waitTime": {"min": 20, "max": 60}
}
```

### URL 批量（账号独立）

```json
{
  "mode": "url",
  "accounts": [
    {
      "name": "账号1",
      "serialNumber": "BROWSER_SERIAL_001",
      "urls": ["https://www.instagram.com/p/ABC123/"]
    }
  ],
  "useAccountUrls": true,
  "comments": ["Nice!"],
  "maxComments": 30,
  "commentsPerAccount": 5
}
```

### 养号模式

```json
{
  "mode": "nurture",
  "accounts": [
    {"name": "账号1", "serialNumber": "BROWSER_SERIAL_001"}
  ],
  "nurtureTopics": ["#fashion", "#style"],
  "nurturePostsPerTopic": 10,
  "nurtureLikeRate": 70,
  "nurtureCommentRate": 20,
  "maxComments": 50
}
```

## 风控建议

⚠️ **重要**：Instagram 对自动化行为有严格限制，请务必遵守：

| 模式 | 等待时间 | 每日上限 | 建议 |
|------|----------|----------|------|
| 关键词搜索 | 20-60秒 | 50条/账号 | 新账号先养号3-5天 |
| URL批量 | 40-90秒 | 30条/账号 | 使用账号独立URL |
| 养号模式 | 10-30秒 | 50个帖子/账号 | 最安全模式 |

### 通用建议

- 新账号前 3 天不要评论，只使用养号模式
- 评论内容多样化，使用 AI 或 10+ 条不同评论
- 每个账号使用不同的 AdsPower 浏览器配置
- 分时段操作，避免连续长时间运行
- 定期检查账号状态，发现异常立即停止

## 目录结构

```
insbot-plugin/
├── .claude-plugin/
│   └── plugin.json          # 插件清单
├── agents/
│   └── insbot-agent.md      # 执行代理
├── skills/
│   ├── keyword-mode/SKILL.md
│   ├── url-mode/SKILL.md
│   └── nurture-mode/SKILL.md
├── commands/
│   ├── insbot.md
│   ├── keyword.md
│   ├── url.md
│   └── nurture.md
└── README.md
```

## 故障排查

### API 服务未启动

```bash
# 启动服务
cd insta_bot_ui
node api/server.js
```

### 端口被占用

修改 `insta_bot_ui/api/server.js` 中的端口号。

### AdsPower 连接失败

1. 检查 AdsPower 是否运行
2. 检查 API 端口（默认 50325）
3. 验证浏览器序列号是否正确

### 任务卡住

```bash
# 停止任务
/insbot:insbot 停止当前任务

# 或直接调用 API
curl -X POST http://localhost:3000/api/stop
```

## 开发

### 添加新命令

1. 在 `commands/` 创建 `.md` 文件
2. 添加 frontmatter（description）
3. 编写使用说明

### 添加新 Skill

1. 在 `skills/` 创建目录
2. 创建 `SKILL.md` 文件
3. 更新 Agent 文档引用

## 许可

MIT License

## 相关链接

- [InstaBot 主项目](https://github.com/your-repo/insta-bot)
- [AdsPower 官网](https://www.adspower.net/)
- [Claude Code 文档](https://claude.ai/claude-code)
