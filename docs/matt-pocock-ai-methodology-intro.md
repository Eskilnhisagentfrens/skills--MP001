# Matt Pocock AI Coding Methodology — Introduction / 介绍 / はじめに

> Source: YouTube《Full Walkthrough: Workflow for AI Coding》— Matt Pocock @ AI Engineer (01:36:29)
> Date: 2026-04-29

---

## English

### Overview

Matt Pocock's AI coding methodology reframes what it means to develop software with AI. The central idea is simple but counterintuitive: **AI coding is not "spec in, code out."** It is a disciplined collaboration where humans own direction, boundaries, and taste — while agents handle high-frequency execution within a tight feedback loop.

Developers are not replaced by AI; they are elevated to the role of **technical director** — designing tasks, feedback mechanisms, module boundaries, and review processes.

### Three Core Beliefs

**1. LLMs have a Smart Zone and a Dumb Zone.**
Even if a model claims to support 1M tokens, its reliable reasoning window is roughly the first 100k. Tasks must be scoped small. Feeding an agent an entire system at once is a recipe for degraded output.

**2. The agent is like the protagonist of *Memento*.**
Clearing context returns the agent to its system-prompt baseline. Matt actively prefers clearing over compacting, because compacted summaries carry accumulated bias and "sediment" that pollute future reasoning. Any workflow that only works with a long, unbroken context is fragile by design.

**3. Bad codebases make bad agents.**
Shallow modules, tangled dependencies, unclear boundaries — these problems hurt human developers and hurt agents even more. Investing in architecture *is* investing in agent productivity.

### The Workflow at a Glance

The methodology follows a structured loop:

1. **Grill Me** — A one-question-at-a-time requirements interrogation, where the AI proposes answers to reduce cognitive load on the human. The goal is shared understanding, not document generation.
2. **PRD** — A destination document capturing the *why*, *who*, *what*, and — critically — the *out of scope*. If grilling went well, the PRD mostly codifies alignment already reached.
3. **Kanban Decomposition** — Tasks broken into a dependency graph (DAG), not a linear phase plan. Each issue is tagged with its blockers and whether it is AFK-eligible.
4. **Vertical Slicing** — Every issue cuts across the full stack (schema → service → business logic → UI → end-to-end test), delivering a runnable, testable slice — never a horizontal layer in isolation.
5. **TDD Loop** — Red → Green → Refactor. The failing test must exist and be observed to fail *before* the implementation begins. This is the agent's steering wheel; without it, agents write tests that confirm their own code rather than validate the requirement.
6. **AFK Implementation** — Once PRD and Kanban are ready, the agent runs autonomously: pick unblocked issue → TDD → tests/typecheck/lint → commit → repeat. Matt advises starting with a single `once.sh` run before enabling the full loop.
7. **Clean-Context Review** — A fresh agent, with no memory of the implementation, reviews the diff against explicit standards. Author bias is structurally eliminated.
8. **Human QA** — Product experience and taste cannot be delegated. The human has the final word.

### Key Engineering Principle: Deep Modules

Drawing on John Ousterhout's *A Philosophy of Software Design*, Matt advocates for **deep modules** — narrow public interfaces over rich internal capability. For agents, this means less context burden, cleaner boundaries, and stronger isolation for testing. Humans design the interface; agents implement the internals.

### The One Rule

> **Scope the task, not the context.**

A smaller, well-bounded task with a strong feedback loop will outperform a large, open-ended prompt every time. The human's highest-leverage contribution is not writing prompts — it is designing the conditions under which the agent can succeed autonomously.

---

## 中文

### 概述

Matt Pocock 的 AI 编码方法论从根本上重新定义了"与 AI 协作开发软件"的含义。核心观点简单却反直觉：**AI 编码不是"输入规格、输出代码"**，而是一种有纪律的协作——人类负责定义方向、边界与品味，Agent 在清晰的反馈循环中高频执行。

开发者不会被 AI 取代，而是升级为**技术导演**——设计任务、设计反馈机制、设计模块边界、设计审查流程。

### 三个底层认知

**1. LLM 有"聪明区"和"愚蠢区"。**
即便模型声称支持 1M token，真正可靠的推理窗口约为前 100k。任务必须切小。把整个系统一口喂给 Agent，输出质量必然下降。

**2. Agent 像《记忆碎片》的主角。**
清空上下文后，Agent 回到系统提示词的初始状态。Matt 主动偏好清空而非压缩（compact），因为压缩摘要会携带偏差和"沉积物"，污染后续判断。任何依赖长期不中断上下文才能运行的工作流，本质上都是脆弱的。

**3. 差的代码库造就差的 Agent。**
浅模块、依赖混乱、边界不清——这些问题对人类开发者不友好，对 Agent 更是加倍不友好。投资代码架构，就是在投资 Agent 生产力。

### 工作流总览

该方法论遵循一个结构化循环：

1. **Grill Me（需求追问）** — 一次只问一个问题，AI 主动给出推荐答案以降低人类认知负担。目标是达成共同理解，而非生成文档。
2. **PRD（目的地文档）** — 记录"为什么、为谁、做什么"，以及最关键的——**明确不做什么（Out of Scope）**。追问做得好，PRD 主要是固化已对齐的共识。
3. **Kanban 拆解** — 任务以依赖图（DAG）形式拆解，而非线性阶段计划。每个 Issue 标注阻塞关系和是否可 AFK 执行。
4. **垂直切片** — 每个 Issue 跨越完整技术栈（schema → service → 业务逻辑 → UI → 端到端测试），交付一个可运行、可测试的最小闭环，而非孤立的技术层。
5. **TDD 循环** — 红灯 → 绿灯 → 重构。失败的测试必须先存在并被观察到失败，再写实现。这是 Agent 的方向盘；没有它，Agent 会写出"配合自身代码"的假测试，而非验证业务逻辑。
6. **AFK 执行** — PRD 和 Kanban 就绪后，Agent 自主运行：选取未阻塞 Issue → TDD → 测试/类型检查/Lint → commit → 循环。Matt 建议先用 `once.sh` 单次运行观察行为，再开启完整循环。
7. **隔离审查** — 一个全新的 Agent（无任何实现记忆）对照明确规范审查 diff，从结构上消除"作者偏见"。
8. **人类 QA** — 产品体验与品味无法外包，人类拥有最终决定权。

### 核心工程原则：深模块

引用 John Ousterhout《软件设计哲学》，Matt 倡导**深模块**——对外接口窄、内部能力深。对 Agent 而言，这意味着更轻的上下文负担、更清晰的边界、更强的测试隔离性。人类设计模块接口，Agent 实现模块内部。

### 一条总则

> **缩小任务边界，而非扩大上下文。**

边界清晰、反馈强的小任务，永远优于模糊宽泛的大提示词。人类最高价值的贡献，不是写提示词——而是设计让 Agent 能够自主成功的条件。

---

## 日本語

### 概要

Matt Pocock の AI コーディング方法論は、「AI とともにソフトウェアを開発する」という行為の本質を根本から捉え直すものです。中心的なアイデアはシンプルですが、直感に反しています。**AI コーディングとは「仕様を入力してコードを出力する」ものではありません。** それは規律ある協働であり、人間が方向性・境界・品質感覚を担い、エージェントは明確なフィードバックループの中で高頻度の実行を担います。

開発者は AI に置き換えられるのではなく、**テクニカルディレクター**へと昇格します——タスクを設計し、フィードバックの仕組みを設計し、モジュール境界を設計し、レビュープロセスを設計する存在として。

### 三つの根本的な認識

**1. LLM には「スマートゾーン」と「ダムゾーン」がある。**
モデルが 1M トークンに対応すると謳っていても、信頼できる推論ウィンドウは最初の約 100k トークンに限られます。タスクは小さく区切らなければなりません。システム全体をエージェントに一度に与えれば、出力品質は必然的に低下します。

**2. エージェントは映画『メメント』の主人公に似ている。**
コンテキストをクリアすると、エージェントはシステムプロンプトの初期状態に戻ります。Matt は「コンパクト（圧縮）」よりも「クリア（消去）」を積極的に好みます。圧縮された要約には偏りや「堆積物」が含まれており、その後の判断を汚染するからです。長期間中断なくコンテキストを保持しなければ動かないワークフローは、設計上脆弱です。

**3. 悪いコードベースは悪いエージェントを生む。**
浅いモジュール・依存関係の混乱・不明確な境界——これらの問題は人間の開発者にも害を与えますが、エージェントにはさらに大きなダメージを与えます。アーキテクチャへの投資は、エージェントの生産性への投資です。

### ワークフローの概要

この方法論は構造化されたループに従います。

1. **Grill Me（要件の深掘り）** — 一度に一つの質問を行い、AI が推奨回答を提示することで人間の認知負荷を軽減します。目標はドキュメントの生成ではなく、共通理解の達成です。
2. **PRD（目的地ドキュメント）** — 「なぜ・誰のために・何を」を記録し、最も重要な**スコープ外（Out of Scope）**を明示します。深掘りがうまくいっていれば、PRD はすでに合意された内容を文書化するだけです。
3. **カンバン分解** — タスクは線形フェーズ計画ではなく、依存グラフ（DAG）として分解されます。各 Issue にはブロッカーと AFK 実行可否が明示されます。
4. **垂直スライス** — 各 Issue はスタック全体を縦断します（スキーマ → サービス → ビジネスロジック → UI → E2E テスト）。孤立した技術レイヤーではなく、実行・テスト可能な最小の閉ループを届けます。
5. **TDD ループ** — レッド → グリーン → リファクタリング。実装を書く前に、失敗するテストを先に作成し、失敗することを確認しなければなりません。これがエージェントのハンドルです。これなしでは、エージェントは要件を検証するのではなく、自分のコードを肯定するテストを書いてしまいます。
6. **AFK 実装** — PRD とカンバンの準備ができたら、エージェントが自律的に動作します。ブロックされていない Issue を選択 → TDD → テスト/型チェック/Lint → コミット → 繰り返し。Matt はフルループを有効にする前に、`once.sh` で単回実行して動作を観察することを推奨しています。
7. **クリーンコンテキストレビュー** — 実装の記憶を一切持たない新しいエージェントが、明確な基準に照らして差分をレビューします。著者バイアスを構造的に排除します。
8. **人間による QA** — プロダクト体験と品質感覚は委譲できません。最終的な判断は人間が下します。

### コアエンジニアリング原則：深いモジュール

John Ousterhout の著書『ソフトウェアデザインの哲学』を引用し、Matt は**深いモジュール**を提唱します——外部インターフェースは狭く、内部機能は豊かに。エージェントにとって、これはコンテキストの負荷軽減・明確な境界・テスト分離の強化を意味します。人間がモジュールのインターフェースを設計し、エージェントが内部を実装します。

### 一つの原則

> **コンテキストを広げるのではなく、タスクを絞り込む。**

境界が明確で強いフィードバックループを持つ小さなタスクは、曖昧で大きなプロンプトに常に勝ります。人間の最も高い価値の貢献は、プロンプトを書くことではなく——エージェントが自律的に成功できる条件を設計することです。
