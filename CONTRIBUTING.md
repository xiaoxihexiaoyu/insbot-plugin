# 贡献指南

感谢你对 InstaBot Claude Code 插件的关注！

## 如何贡献

### 报告问题

请在 GitHub Issues 中报告问题，包含：
- 问题描述
- 复现步骤
- 预期行为
- 实际行为
- 环境信息（OS、Claude Code 版本）

### 提交代码

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/your-feature`
3. 提交更改：`git commit -m "feat: add some feature"`
4. 推送分支：`git push origin feature/your-feature`
5. 创建 Pull Request

### 代码规范

- **Commit Message**：使用 Conventional Commits 格式
  - `feat:` 新功能
  - `fix:` 修复问题
  - `docs:` 文档更新
  - `refactor:` 重构
  - `test:` 测试相关

- **文件命名**：
  - Command: `commands/<name>.md`
  - Agent: `agents/<name>-agent.md`
  - Skill: `skills/<category>/SKILL.md`

- **Frontmatter**：
  - Commands 必须有 `description`
  - Agents 必须有 `name`, `description`, `tools`, `model`

### 开发环境

1. 安装 Claude Code
2. 本地测试插件：
   ```bash
   claude --plugin-dir ./insbot-plugin
   ```

3. 确保 API 服务器运行：
   ```bash
   cd insta_bot_ui
   node api/server.js
   ```

### 文档

- 更新 README.md 说明新功能
- 添加 SKILL.md 文档说明参数
- 更新 CHANGELOG.md 记录变更

## 许可

提交代码即表示你同意将代码以 MIT 许可证发布。
