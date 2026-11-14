# HiSparse / PCP 设计笔记

[网页目录](https://zyz111222.github.io/hisparse-design-notes/) · [HiSparse](https://zyz111222.github.io/hisparse-design-notes/hisparse.html) · [PCP](https://zyz111222.github.io/hisparse-design-notes/pcp.html) · [HiSparse + PCP](https://zyz111222.github.io/hisparse-design-notes/hisparse-pcp.html)

按三个主题独立成篇：HiSparse 的缓存与请求生命周期；不开 HiSparse 的 PCP 切分、KV 交换与恢复；两者组合的布局、同步、graph / MTP 与混部 / PD 边界。保留旧版全部章节与源码证据，旧网址及其章节锚点自动转到对应新页。

核对版本：Core `24420b7a341af37a9bc3186e6fc6062512e0aa58`；Ascend PCP `14a31903a98f2b913c8fbe2bcb02d37a544889ba`；基础 `66748c3c4ab730509e8104a201767a2add4a6f5d`。不是最新 main 能力清单，也不新增设备或性能验收结论。当前 Ascend PCP adapter 拒绝 MultiConnector，不能将 Core PD 接口视为 PD + HiSparse + PCP 已打通。

各页均内嵌样式、SVG 图与裁剪源码，无 CDN；下载 HTML 并保存在同目录可离线阅读。已检查桌面 / 窄屏结构、相对链接、章节导航和源码展开；未做截图视觉校验。

关联：[基础 #20926](https://github.com/vllm-project/vllm-ascend/pull/20926)、[官仓 PCP #21892](https://github.com/vllm-project/vllm-ascend/pull/21892)、[个人 fork PCP #1](https://github.com/zyz111222/vllm-ascend/pull/1)。关联不表示已合入。
