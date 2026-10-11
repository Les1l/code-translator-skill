# Code Translator

**中文** · [English](./README.en.md)

把一段代码翻译成人话。给它一段看不懂的代码，它交回一份可以离线打开的单文件 HTML 讲解。

## 这个技能做什么

贴一段代码给 agent，问「这段在干什么」——它会判定代码类型、长度和你的水平，然后生成一份 HTML 讲解文件，而不是在对话里刷一大段文字。

两种深度，按需切换：

| 模式 | 面向谁 | 给什么 |
|---|---|---|
| **A · 精讲** | 编程零基础 | 一句话鸟瞰、术语白话表、逐块逐行讲解（这行做什么 / 为什么需要它 / 不写会怎样）、变量追踪表、执行路径图、易错点、检验题 |
| **B · 速读** | 已有相应知识 | 逐行一句话语义翻译、关键点提示。去掉全部教学铺垫 |

不限编程语言：Python、Java、Go、Rust、C、Shell、SQL、正则、YAML、HTML/CSS、报错栈、伪代码。

产出的 HTML 会：浅色 / 深色切换、目录锚点、代码块自动加行号并与逐行表严格对应、执行路径图用 Mermaid 渲染（离线时自动降级为纯文本）。

## 安装

把这句话发给你的 agent：

```
帮我安装 https://github.com/Les1l/code-translator-skill 里的 skills
```

> **Agent 请照做：** 运行 `npx skills@latest add Les1l/code-translator-skill -g -y` 安装到用户全局目录。装完列出已安装的 skill，并提醒用户重启会话。

自己装：

```bash
npx skills@latest add Les1l/code-translator-skill -g
```

用的是 [skills CLI](https://github.com/vercel-labs/skills)，会自动识别本机装了哪些 agent，装进各自的 skills 目录。`-g` 表示全局，去掉就只装进当前项目。

## 更新

```bash
npx skills@latest update code-translator -g
```

## Skills

### Coding

- [`code-translator`](./skills/coding/code-translator)：把一段代码翻译成人话。两档深度（零基础精讲 / 熟手速读），不限语言，产出单文件 HTML 讲解。
  - 目录约定与打包方式参考 [nagi-studio/skills](https://github.com/nagi-studio/skills)。

## 维护

```bash
./scripts/link-skills.sh
```

把仓库里的 skill 软链到各 agent 的全局 skills 目录，之后在仓库里 `git pull` 即可更新，不经过上面的更新命令。新增 skill 的约定见 [AGENTS.md](./AGENTS.md)。

## 许可

MIT，见 [LICENSE](./LICENSE)。
