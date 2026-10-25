# Claude Skills Marketplace

个人 Skills 市场仓库（`ElvishScout/claude-skills`），同时兼容 **Claude Code Plugin Marketplace** 与 **OpenCode HTTP Skill Catalog**。

## 快速使用

### 在 Claude Code 中使用

#### 1. 添加 Marketplace

在 Claude Code 会话中运行：

```text
/plugin marketplace add ElvishScout/claude-skills
```

或在终端使用 CLI：

```bash
claude plugin marketplace add ElvishScout/claude-skills
```

#### 2. 安装指定 Skill

```text
/plugin install example-skill@claude-skills
```

或使用 CLI：

```bash
claude plugin install example-skill@claude-skills
```

#### 3. 更新 Marketplace

```text
/plugin marketplace update claude-skills
```

---

### 在 OpenCode 中使用

#### 方式 A：远程 HTTP Catalog（免克隆）

在 `~/.config/opencode/opencode.jsonc`（全局）或项目的 `opencode.jsonc` 中添加：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "skills": [
    "https://raw.githubusercontent.com/ElvishScout/claude-skills/main/skills/"
  ]
}
```

#### 方式 B：本地目录直连

如果已克隆本仓库到本地，直接指向 `skills` 目录即可：

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "skills": [
    "D:/Projects/claude-skills/skills"
  ]
}
```

---

## 目录结构

```text
claude-skills/
├── .claude-plugin/
│   └── marketplace.json        # Claude Code Marketplace 索引配置
├── skills/
│   ├── index.json              # OpenCode HTTP Catalog 索引配置
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

2. **注册到 Claude Code**：在 `.claude-plugin/marketplace.json` 的 `plugins` 数组中添加：

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

3. **注册到 OpenCode Catalog**：在 `skills/index.json` 的 `skills` 数组中添加（更新内容时递增 `version`）：

   ```json
   {
     "name": "your-skill-name",
     "version": "1",
     "files": [
       "SKILL.md"
     ]
   }
   ```

4. 本地校验配置并推送到 GitHub：

   ```bash
   claude plugin validate .
   git add .
   git commit -m "feat: add your-skill-name"
   git push
   ```
