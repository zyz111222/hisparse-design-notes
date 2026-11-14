# HiSparse 与 PCP 设计导读

以固定源码解释 vLLM Core、vLLM Ascend、PCP 和 PD 分离的职责及边界。

**[查看 / 下载 HTML](hisparse-pcp-guide.html)**：在 GitHub 文件页点击下载按钮，保存后用浏览器打开。单文件离线可读；源码链接需联网。当前仓库为私有仓库。

- 核对日期：2026-11-14。
- Core：`24420b7a341af37a9bc3186e6fc6062512e0aa58`，本次未修改。
- Ascend 基础：`66748c3c4ab730509e8104a201767a2add4a6f5d`；PCP：`14a31903a98f2b913c8fbe2bcb02d37a544889ba`。
- 关联：[基础 PR #20926](https://github.com/vllm-project/vllm-ascend/pull/20926)、[Ascend PCP PR #21892](https://github.com/vllm-project/vllm-ascend/pull/21892)、[个人 fork PCP-only 对比 #1](https://github.com/zyz111222/vllm-ascend/pull/1)。

本轮直接覆写 Core 的 `_build_load_kwargs()` 扩展点，继承加载时序；query/write 布局分离仍在 Ascend worker patch 中。基础 PR 最新 head `0ecd9217` 尚未重放到当前分支；文档区分现有能力与后续工作。

验证：71 项 CPU 回归通过，NPU 未初始化；HTML 离线交互和两种视口结构检查通过，未做图片视觉检查。本轮未重跑 NPU；设备验证仍对应先前的 `e48dc6a5`。
