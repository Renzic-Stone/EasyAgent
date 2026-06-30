# EasyAgent

> **用户只需要知道一个名字。Agent 搞定剩下的。**

EasyAgent 是一套**设计范式**，不是框架。它定义了一种 AI Agent 产品的组织方式：
用户只需说一个名字 → Agent 自主完成配置 → 用户只做最后一步手动操作。

## 核心哲学

### 一句话定义

> **用户知道项目叫什么 → 告诉 Agent → Agent 自动配置到可用 → 用户只需登录。**

### 三要素

一个 EasyAgent 产品由三个文件构成：

```
repo-name/
├── README.md          # ① 配置入口（写给 Agent 读的安装指令）
├── template/          # ② 模板（Agent 可读的代码骨架）
└── servers/           # ③ 成品（模板的具象化 = 即用型 skill）
```

#### ① README = 配置入口

README 的主要读者是 **AI Agent**，不是人类。它必须包含一段 **Agent 安装流程**：

> 告诉 Agent：「帮我装 EasyAgent-XXX，项目在 [路径]。」
> Agent 请按以下流程执行：
> 1. 询问用户需要哪些功能
> 2. 自动安装依赖（npm/pip 等）
> 3. 注册 MCP / 配置环境
> 4. 调 doctor() 自检
> 5. 引导用户完成最后手动操作

用户看到的体验：

```
你: "帮我装 EasyAgent-SocialMedia"
Agent: "你需要哪些平台？B站、X、小红书、Reddit？"
你: "B站和 X"
Agent: "B站已就绪。正在安装 OpenCLI... 装好了。
       请装 Chrome 扩展，登录 x.com，登录完告诉我。"
你: "好了"
Agent: 全部配置完成 ✅
```

#### ② 模板 = 扩展口

Agent 读模板就能生成新的 skill。模板不需要文档——代码结构本身就是文档。

```
template/
└── template.py         # 代码骨架 + 注释标注可替换部分
```

#### ③ 成品 = 样板

成品是模板的具象化实例，既是即用型 skill，也是开发者的参考实现。

```
servers/
├── example_a.py        # Class A-1 样板
└── example_b.py        # Class B-1 样板
```

## 四象限分类

EasyAgent 把功能项分为四个象限：

```
                    数据干净（透传）    需数据清洗（提取/去冗余）
                    ─────────────────   ─────────────────────────
零配置（公开 API）    A-1                A-2
需登录（Cookie/CLI）  B-1                B-2
```

任何功能项都可以归入某个象限，从而决定：
- A 系列：纯 HTTP/公开 API，零配置，注册即用
- B 系列：需要登录态，需要引导用户手动登录
- 系列 1：原始数据可用，直接透传
- 系列 2：原始数据冗余，需要清洗提取

## 配置模型

```
用户 → "帮我装 XXX"
        ↓
Agent 读 README → 问用户要什么
        ↓
Agent 自动执行：安装依赖 → 注册 → 自检
        ↓
Agent 引导用户完成最后手动步骤（装扩展、登录）
        ↓
全部就绪 ✅
```

Agent **自动完成**的部分：
- 安装底层 CLI（npm/pip）
- 注册 MCP 到网关
- 调 doctor() 确认状态

用户**唯一手动**的部分（B 系列）：
- 装 Chrome 扩展
- 登录对应网站

## EasyAgent 产品清单

| 产品 | 描述 | 状态 |
|------|------|------|
| [EasyAgent-SocialMedia](https://github.com/Renzic-Stone/EasyAgent-SocialMedia) | B站 / X / 小红书 / Reddit | ✅ 已发布 |
| EasyAgent-DevTools | GitHub / GitLab / Stack Overflow | 📋 待创建 |
| EasyAgent-News | Hacker News / 知乎 / V2EX / 科技媒体 | 📋 待创建 |

## 创造一个新 EasyAgent 产品

### 对人类开发者

```
1. mkdir EasyAgent-YourIdea
2. 复制 template/template.py
3. 写 README（含 Agent 安装流程）
4. 实现功能项
5. 发到 GitHub
```

### 对 AI Agent

告诉你的 Agent：

> 「帮我看一下 EasyAgent 范式的 README，我想创建一个 EasyAgent-XXX。」

Agent 读了这个文件就知道该做什么。

## License

MIT — 你可以自由使用、修改、商用，只需保留原始版权声明。
