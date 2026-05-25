# linus-review · Claude Code Skill

Linus Torvalds 风格的代码审计 skill。手动调用，专门审视 AI（或人）刚写完的代码，
揪出讨好型设计、过度抽象、防御性垃圾、假可靠的错误处理，以及十年后没人敢碰的屎山苗头。

> "AI 写代码最大的问题不是不够聪明，是太会讨好人。它会把烂设计包装成'优雅方案'，
> 用抽象和模式掩盖工程上的懒惰，最后留下一个十年后没人敢碰的屎山。"

这个 skill 反过来做：不教 AI 怎么写代码，给它灌一套**工程价值观**——简单胜过聪明，
显式胜过隐式，无聊胜过花哨，数据结构第一，错误路径必须可靠，永不破坏既有调用者。

## 安装

```bash
cd ~/.claude/skills
git clone https://github.com/chenly255/claude-skill-linus-review linus-review
```

或者直接复制 `SKILL.md` 到 `~/.claude/skills/linus-review/SKILL.md`。

## 使用

在 Claude Code 里输入以下任一触发词：

- `Linus 审一下`
- `骂一下我的代码`
- `code review`
- `代码审计`
- `看看这段代码有没有屎山`
- `AI 写的代码靠谱吗`
- `过度设计了吗`
- `能活十年吗`
- `/linus-review`

然后给 skill 喂代码（文件路径 / git diff / 直接粘贴片段）。

## 审计输出

每次审计严格按以下结构输出：

1. **审视场景** — 跑在哪、谁维护、负载、失败代价（缺哪条要补哪条）
2. **整体品味评分** — 好品味 ✓ / 凑合用 ~ / 屎山预警 ✗
3. **致命问题** — 按严重程度排，带定位 + 现实后果
4. **AI 反模式命中清单** — 12 项常见 AI 代码病灶逐条打钩
5. **改进方向** — 每条带"为什么"，不写"是什么"
6. **拒绝的"聪明"改法** — 预判讨好型 AI 会怎么改坏
7. **是否需要 codex 二审** — 避免 AI 互相讨好的盲点

## 与 codex review 的协同

Claude 写代码、Claude 自审，结论天然偏向讨好——这是 Claude Code 工作流的固有盲点。
当 stakes 足够高时（生产代码、并发、安全敏感、性能关键），skill 会建议用 `/codex:rescue`
让 codex 子代理做独立第二意见。两个独立底座的判断撞出火花的地方，往往是真问题。

## 设计原则

- **手动触发**：description 围绕显式调用关键词，不会因为你在写代码就自动跳出来。
- **强制场景澄清**：脱离场景谈代码就是耍流氓。缺场景信息会被明确标记。
- **AI 反模式专项**：12 条常见的 Claude/GPT 代码病灶（防御性 try、过度抽象、伪命名、
  假错误处理、配置幻觉、mock 套娃、类型体操……），逐条扫。
- **不安慰，不水军**：直接讲哪里烂、为什么烂。技术判断不为了"友好"打折。
- **不主动改代码**：审计 skill 只输出报告，是否按建议改由人决定。

## License

MIT — 拿去用，别拿去坑队友。

## 致谢

灵感来自云中江树的 Linus Torvalds 数字分身 prompt，结合 Linus 在 Linux 内核维护 30 年
反复强调的「good taste」、「never break userspace」、「bad programmers worry about
the code, good programmers worry about data structures」三大信条，并针对 AI 写代码
时代的新型反模式做了特化扩展。
