# HiSparse 设计详解

[直接阅读网页](https://zyz111222.github.io/hisparse-design-notes/hisparse-pcp-guide.html)

个人公开设计笔记，按固定源码核对；单文件 HTML，可下载后离线阅读，无外部依赖。

20 章、13 张内嵌图，包含调度与执行类图、缓存页状态、初始化及逐层执行时序、stream 同步、PCP 布局、混部与 PD 分离设计；74 段源码附版本、真实行号和链接，默认折叠。

核对版本：

- vLLM Core：`24420b7a341af37a9bc3186e6fc6062512e0aa58`
- Ascend PCP：`14a31903a98f2b913c8fbe2bcb02d37a544889ba`
- Ascend 基础：`66748c3c4ab730509e8104a201767a2add4a6f5d`

区分 Core 接口能力、Ascend 分支实现和实际验收。当前 PCP adapter 拒绝 MultiConnector，不能将 Core 的 PD 接口视为 Ascend PD + HiSparse + PCP 已打通。本文是代码设计分析，不新增设备或性能验收结论。

关联：[基础 #20926](https://github.com/vllm-project/vllm-ascend/pull/20926)、[官仓 PCP #21892](https://github.com/vllm-project/vllm-ascend/pull/21892)、[个人 fork PCP 增量 #1](https://github.com/zyz111222/vllm-ascend/pull/1)。以上为关联链接，不代表已合入。

本地浏览器完成结构和交互检查；未做截图视觉校验。
