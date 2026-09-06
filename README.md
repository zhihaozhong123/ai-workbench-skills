# ai-workbench-skills

智作台（ai-workbench）技能集中仓库 — 所有业务技能按分类存放，供内部维护人员引入到 ai-workbench 技能市场。

## 仓库结构

```
ai-workbench-skills/
├── wechat/                      # 分类：公众号
│   └── wechat-article-publish/  # 技能：公众号文章批量发布
├── tool/                        # 分类：工具
├── content/                     # 分类：内容
├── data/                        # 分类：数据
└── README.md
```

每个技能目录遵循 [skill-scaffold](https://github.com/zhihaozhong123/skill-scaffold) 模板结构：

```
<skill-slug>/
├── manifest.json          # 技能元数据（权威）
├── SKILL.md               # 给 Agent 的技能说明
├── AGENT.md               # 系统提示词
├── README.md              # 用户说明
├── CHANGELOG.md           # 变更日志
├── requirements.txt       # 技能特有依赖
├── scripts/
│   ├── main.py            # CLI 入口
│   ├── cli/app.py         # 参数分发
│   ├── service/           # 业务逻辑
│   └── util/              # 工具
├── references/CLI.md      # CLI 契约文档
└── tests/                 # 单元测试
```

## 分类约定

| 分类目录 | manifest.category | 说明 |
|----------|-------------------|------|
| `wechat/` | 公众号 | 微信公众号相关技能 |
| `tool/` | 工具 | 通用工具类技能 |
| `content/` | 内容 | 内容生成/处理类技能 |
| `data/` | 数据 | 数据查询/处理类技能 |

新增分类时，在此表登记并创建对应目录。

## 内外协作流程

### 外来开发人员

1. 克隆 [skill-scaffold](https://github.com/zhihaozhong123/skill-scaffold) 模板
2. 按模板规范开发业务技能
3. 提交 Pull Request 到本仓库（放到对应分类目录下）

### 内部维护人员

1. 审核外来开发人员提交的技能代码
2. 本地测试通过后合并到本仓库
3. 在 ai-workbench 中执行引入脚本，将技能安装到技能市场

## 技能规范

- 必须遵循 XST-Skill v1 契约（stdin JSON → stdout JSON）
- `manifest.json` 的 `category` 字段须与所在分类目录一致
- 每个技能须包含单元测试（`tests/`）
- 凭证不进技能包，通过 `env_whitelist` 由宿主注入
