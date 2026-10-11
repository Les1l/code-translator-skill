# Agent 维护约定

这个仓库存放 agent skills。改动它时遵守下面的约定。

目录布局、打包方式与这份约定的骨架参考 [nagi-studio/skills](https://github.com/nagi-studio/skills)（MIT）。

## 目录结构

```
skills/<category>/<skill-name>/
  SKILL.md              # 必需。frontmatter 放 name + description
  agents/openai.yaml    # 必需。Codex 等 harness 的展示信息与调用策略
  references/*.md       # 可选。按需加载的长文档，SKILL.md 里用相对链接指向
  assets/*              # 可选。产出物模板，不加载进上下文，直接复制使用
```

`skills/<category>/` 下的每个目录只要含 `SKILL.md` 就会被 `scripts/link-skills.sh` 链出去。

仓库根目录另有 `.claude-plugin/`、`.gitattributes`、`.gitignore` 与 `README*.md`。其中 `.gitattributes` 用来锁 `*.sh` 的换行符为 LF——少了它，在 Windows 上编辑过脚本再提交，会让 Linux / macOS 的克隆者拿到 CRLF 而无法执行。

## SKILL.md 规则

- frontmatter 的 `name` 用 kebab-case，和目录名一致。
- `description` 要写清**什么时候用**，包含用户可能说的原话触发词（中英文都列），因为模型靠它决定是否调用。
- 同时写**反向边界**——把相邻但**不该**触发的场景列出来（例如「让 agent 写代码 / 修 bug / 优化重构时不触发」），这是减少误调用最有效的一招。
- 正文用祈使句写给 agent 看，不是写给人看的文档。
- 单文件超过约 500 行就拆到 `references/`，主文件只留路由和不可协商的规则。
- 引用 reference 时写相对路径链接，并明确说「读完再回复」。

## agents/openai.yaml 规则

```yaml
interface:
  display_name: "Human Readable Name"
  short_description: "一句话说明"
  default_prompt: "可选，用户点按钮时的默认输入"
policy:
  allow_implicit_invocation: false # 只在「必须用户显式调用」时加
```

本仓库的 skill 都应能被自然语言隐式触发，因此**不加** `policy` 段。

## assets/ 里的模板

- 模板是给产出用的，不是给人读的。占位符统一用 `{{UPPER_SNAKE}}`，替换完不应残留 `{{ }}`。
- 模板顶部用注释写清用法；样式与脚本全部内联，保证产物**可离线打开**。
- 外部依赖只允许来自稳定 CDN，且必须有加载失败的降级路径。
- 改模板的样式或脚本前想清楚：所有历史产物共用同一套观感，改了就前后不一致。要改就批量重生。

## 新增 skill 后

1. 把路径加进 `.claude-plugin/plugin.json` 的 `skills` 数组。
2. 在 `README.md` 和 `README.en.md` 的对应分类下各加一行说明。
3. 提 PR 前先跑一遍 `./scripts/link-skills.sh`，在真实任务上试用过再合并。

## 隐私

skill 内容会公开。提交前确认没有个人姓名、邮箱、本地绝对路径、机构内部信息、token 或 API key。示例代码和产物文件里出现的真实路径、真实姓名也要一并清掉。
