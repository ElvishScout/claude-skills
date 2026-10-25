# Claude Skills Marketplace

个人 Claude Code Skills 市场仓库（`ElvishScout/claude-skills`），用于集中管理、分发和安装自定义 Claude Code Skills。

## 快速使用

### 1. 添加 Marketplace

在 Claude Code 会话中运行：

```text
/plugin marketplace add ElvishScout/claude-skills
```

或在终端使用 CLI：

```bash
claude plugin marketplace add ElvishScout/claude-skills
```

### 2. 安装常用或指定 Skill

```text
/plugin install example-skill@claude-skills
```

或使用 CLI：

```bash
claude plugin install example-skill@claude-skills
```

### 3. 更新 Marketplace

```text
/plugin marketplace update claude-skills
```

## 目录结构

```text
claude-skills/
├── .claude-plugin/
│   └── marketplace.json        # Marketplace 索引配置
├── skills/
│   └── example-skill/          # 单个 Skill 目录
│       └── SKILL.md            # Skill 定义与指令
└── README.md
```

## 如何新增 Skill

1. 在 `skills/<your-skill-name>/` 下创建 `SKILL.md`：

   ```markdown
   ---
   name: your-skill-name
   description: 简明描述该 Skill 的用途与触发场景
   ---

   # Your Skill Name

   具体指令内容...
   ```

2. 在 `.claude-plugin/marketplace.json` 的 `plugins` 数组中注册该 Skill（或将其归入已有插件包）：

   ```json
   {
     "name": "your-skill-name",
     "description": "简明描述该 Skill 的用途",
     "version": "1.0.0",
     "source": "./",
     "strict": false,
     "skills": [
       "./skills/your-skill-name"
     ]
   }
   ```

3. 本地校验配置是否合法：

   ```bash
   claude plugin validate .
   ```

4. 提交并推送到 GitHub。
