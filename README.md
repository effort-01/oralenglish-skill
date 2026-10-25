# oralenglish-skill

专四口语思辨陪练 Skill（TEM-4 Oral Critical Thinking Practice）。

AI 逐轮抛出一个英文思辨话题，并附带一正一反两句纯英文参考句型；用户口头作答后，AI 输出【我的原句】【优化句】【简短点评】，并提供【继续】（同话题深度追问）与【重新回答】（原地重练）两个选项，实现一轮一轮的循环陪练。

## 项目解决什么问题

专四口语考试的"话题演讲/思辨表达"环节，考生常见困境：

- **开口难**：有观点但不知道怎么说，缺少组织语言的句型支架；
- **中式英语**：一开口就是中文直译（如 `I very like`、`learn knowledge`），搭配和语序不地道；
- **逻辑断层**：观点与理由之间缺连接，表达跳跃、不成结构；
- **练完无感**：练习后不知道自己哪里有问题、怎么改，重复低效。

本项目把思辨陪练固化成一套可重复的对话协议：AI 先出题并给正反句型支架，降低开口门槛；对每次口头作答做"逐字转写 → 仅一版中式英语优化 → 简短点评"，让每次练习都有即时、具体的反馈；用【继续】推进论证深度、【重新回答】支持原地重练，形成一轮一轮可追踪的训练循环。

## 主要功能

- **逐轮出题**：每轮输出一个英文思辨话题（Topic）+ 恰好 2 句纯英文参考句型——一句支持立场（Agree）、一句反对立场（Disagree），可自由选题，也可按用户指定话题出题。
- **原句转写**：①【我的原句】逐字保留用户口述英文，一字不改。
- **单版优化**：②【优化句】仅生成 1 版专四口语水平改写，优先修正中式英语（中文直译语序、中式搭配、逻辑断层、母语负迁移），核心改动加粗，拒绝浅层同义词替换，保留原意、不新增观点。
- **简短点评**：③【简短点评】用中文点明本次中式英语问题并解释原因，同时说明逻辑、句式、用词地道度三方面表现。
- **分支控制**：反馈后给出【继续】/【重新回答】两个选项——【继续】基于当前话题深度追问（具体例子 → 回应反方 → 现实权衡），【重新回答】不换话题原地重练，循环直到选择【继续】。
- **边界引导**：用户中文作答、提问或闲聊时不推进流程，温和引导回当前轮次。
- **零依赖**：纯对话式协议，不抓取网页、不解析 PDF、无图形界面、不处理音频文件。

## 安装方法

- **依赖**：无。不需要安装 Python 包、不需要网络或第三方服务。
- 本项目是纯指令型 Skill，安装 = 把文件夹放到正确的位置：

1. 将 `oralenglish-skill` 文件夹复制到 Agent 客户端的**技能根目录**。豆包客户端的常见技能目录示例：
   - `...\Doubao\skills\`
   - `...\.doubao\agent_mode\workspace\.user_skills\`
   - `...\.doubao\agent_mode\workspace\.skills\`

   具体以你电脑上实际存在的技能目录为准。
2. 重启或刷新客户端，使技能被加载。
3. 在对话中说"开始练口语"即可触发使用。

## 使用方法

1. **触发**：直接说"开始练口语""出个话题""陪我练专四口语"，或指定话题（如"练一下手机成瘾"）。
2. **作答**：AI 输出 **Topic** 和 **2 句参考句型**（一句支持立场、一句反对立场），请参考句型组织语言，用英文口头作答（语音口述由平台转写为文字，也可直接打字）。
3. **反馈**：作答后，AI 依次给出：
   - **①【我的原句】**：原样转写你的回答，一字不改；
   - **②【优化句】**：仅 1 版，专四口语水平改写，优先修正中式英语，改动核心加粗，不做浅层同义词替换；
   - **③【简短点评】**：点明本次中式英语问题并解释原因，同时说明逻辑、句式、用词地道度情况。
4. **选择**：反馈后从两个选项中选择：
   - **【继续】**：基于当前话题深度追问一层，开启新一轮作答（会重新给参考句型）；
   - **【重新回答】**：不换话题，等你重新作答后再做一遍转写、优化、点评，可循环多次。

## 输入输出示例

**用户：** 开始练口语

**AI（出题）：**

> Topic: Should college students take part-time jobs?
>
> Reference Sentences:
> - Agree: "I believe that ___ is worthwhile, because it not only ___ but also ___."
> - Disagree: "While it may seem attractive, I doubt whether ___ is a good idea, since ___."

**用户（口述转写）：**

> I very agree with this, because we can learn many knowledge in the job, and also can make money to reduce parents burden.

**AI（反馈）：**

> ①【我的原句】
> I very agree with this, because we can learn many knowledge in the job, and also can make money to reduce parents burden.
>
> ②【优化句】
> **I strongly agree with this view**, because **we can gain a lot of practical experience from a part-time job**, **and it also allows us to earn some money to ease the financial burden on our parents**.
>
> ③【简短点评】
> - 中式英语："I very agree" 是中文"我非常同意"的直译，very 不能直接修饰动词，应说 strongly/totally agree；"learn many knowledge" 是中式搭配——knowledge 不可数，常与 gain 搭配；"reduce parents burden" 是"减轻父母负担"的逐字翻译，地道说法是 ease the financial burden on our parents。
> - 逻辑：两个理由成立，但 "in the job" 指向含糊，改为 from a part-time job 更清楚。
> - 句式：原句一个长 and 句串到底，优化句拆成"观点 + because 从句 + and 补充"三层，听感更清晰。
> - 用词地道度：gain practical experience、earn some money 比 make money、learn knowledge 更贴口试。
>
> 【继续】 / 【重新回答】

**用户：** 继续 → AI 基于同一话题深度追问（如"能举个具体例子吗？"），重新给出 2 句正反参考句型，进入新一轮。
**用户：** 重新回答 → AI 不换话题，等用户重新作答后再做一遍转写、优化、点评。

## 目录结构

```
oralenglish-skill/
├── SKILL.md            # Skill 核心指令：出题/反馈/分支的完整协议
├── agents/
│   └── openai.yaml     # Skill 元数据与默认触发提示词
├── LICENSE             # MIT 开源许可
└── README.md
```

## 验证

已通过官方 `quick_validate.py` 校验（frontmatter 与命名规范）：

```
$ python quick_validate.py <skill目录>
Skill is valid!
```

当前为本地开发版本：未初始化 Git，未上传 GitHub。
