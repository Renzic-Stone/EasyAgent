# EasyAgent

> **用户最少的操作次数。**

EasyAgent 是一种 AI 产品的组织方式。目标是：用户只需知道一个名字，所有复杂流程由 AI Agent 自动化完成。

## 核心原则

### ① 最小操作次数

一切设计以此为标准。问自己：用户从说出名字到用上，需要动手几次？

```
好的设计：用户说名字 → 回答一次选择题 → 装一个扩展 → 登录 → 用上（3 次）
不好的设计：用户说名字 → 手动装 A → 手动配 B → 手动改 C → 手动注册 → 用上（N 次）
```

每多一次手动操作，就是一次设计失败。

### ② 可选项前置，一次性询问

项目的可选项（平台、功能、模块等）在 README 开头列清。Agent 拿到项目后**一次性问完所有问题**，而不是做完一步再问下一步。

```
✅ 正确：
  Agent: "EasyAgent-SocialMedia 支持以下平台：B站、X、小红书、Reddit。
          你需要哪些？"
  用户: "B站和 X"

❌ 错误：
  Agent: "B站装好了。要装 X 吗？"
  用户: "要"
  Agent: "X 装好了。要装小红书吗？"
  ...
```

一次性询问的好处：
- 用户不需要反复切回对话
- Agent 可以在后台批量处理，不需要每步等用户确认
- 安装过程中如果遇到问题，Agent 可以自动降级

### ③ 自动化灵活构建

不写死安装流程。Agent 根据用户的选择，判断哪些可以直接注册、哪些需要安装依赖、哪些需要引导手动操作。

不同选择走不同路径，但用户看到的始终是同一个简洁对话。

### ④ 模板优先

- **有模板时：** 严格按模板执行。模板是经过验证的最佳实践，不要自己发明流程。
- **没有模板时：** 完成配置后，把流程沉淀为模板。下一个产品就可以复用。

## 一个 EasyAgent 产品的结构

```
repo-name/
├── README.md          ← 配置入口 + 可选项清单（核心）
├── template/          ← 模板（供 Agent 参照构建）
└── servers/           ← 成品（即用型 + 参考实现）
```

### README = 配置入口

写给 Agent 读的。**开头必须有一段可选项清单**，让 Agent 看到后立刻知道要问用户什么。

Agent 拿到项目后，读取 README → 找到可选项清单 → 一次性询问用户。

### 模板 = 扩展基础

Agent 读模板后能理解：某个功能应该怎么实现、结构是什么、哪些部分需要替换。

没模板时，Agent 自动创造一个新模板，沉淀为仓库的一部分。

### doctor() = 自检口

成品必须自带 doctor()。Agent 安装/配置后调它确认一切正常，而不是问用户"好了吗"。

## Agent 执行流程

```
① 用户说 "帮我装 EasyAgent-XXX"
② Agent 找到项目，读 README
③ 从 README 提取可选项清单
④ 一次性问用户：需要哪些？
⑤ 根据选择自动执行：
   - 零配置项 → 直接注册
   - 需依赖项 → 自动安装（npm/pip 等）
   - 需登录项 → 最后集中引导用户
⑥ 调 doctor() 确认全部就绪
⑦ 告知用户：✅ 可以用，只剩 X 需要登录
```

## 项目可以怎么用

### 作为 EasyAgent 产品开发者

```
1. mkdir EasyAgent-你的想法
2. 写 README，开头列清可选项清单
3. 放 template/（可选）
4. 放 servers/ 成品（可选）
5. 发到 GitHub
```

### 告诉你的 AI Agent

> 「帮我看一下 EasyAgent 的 README，我想创建一个 EasyAgent-XXX。」

Agent 读了这个文件就知道：怎么写 README、可选项放哪、流程怎么设计。

## 已发布的 EasyAgent 产品

| 产品 | 描述 | 状态 |
|------|------|------|
| [EasyAgent-SocialMedia](https://github.com/Renzic-Stone/EasyAgent-SocialMedia) | B站 / X / 小红书 / Reddit | ✅ |
| EasyAgent-DevTools | GitHub / GitLab / Stack Overflow | 📋 |
| EasyAgent-News | Hacker News / 知乎 / V2EX | 📋 |

## License

MIT
