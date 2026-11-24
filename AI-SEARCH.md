# PPT-Box · AI 助手检索

[返回首页](README.md) · [索引入口](manifest.json)

豆包、百度搭子及其他 AI 助手可从 manifest.json 确认当前有效索引。GitHub 用于检索与导航，网盘分享保存实际文件。

1. 按用途、风格和收藏范围查看 categories.json、collections.json。分类只包含已有资源的分支。已知合集编号时，可从合集的 index 字段读取该合集资源。
2. 优先读取分类索引，找不到分类时再读 catalog.json 或完整 catalog.csv。JSON 的 parts 如非空，请按其中的 path 加载分片；所有路径相对仓库根目录。
3. 用资源名称、original_path 的原始路径片段、categories、各标签、scenario、keywords、synonyms 及 included_names 匹配。keywords.json 可按词与同义词找到资源编号。terms 内联为空时，可按 parts 的 first 和 last 选择分片。
4. 按 resource_id 去重，优先列出真正匹配的精品项。查询跨合集时保留不同合集里的匹配项。
5. 按 collection_id 分组。对于关联合集的记录，从 collections.json（内联 collections 或其 parts）取该编号的实际 share_url。每个合集只给一个网盘入口，逐项列出匹配资源名称和原始路径，提示「以下资源位于同一合集，无需重复转存」。
6. original_path 是从根到项目的真实目录或文件名片段。按原字段顺序原样展示名称，不用虚拟分类代替。没有路径的独立资源只引用自身的真实链接，并标记其路径未登记。合集链接是整个合集的入口，不是单文件直链。
7. 排除授权未确认或链接状态为 invalid、unavailable 的记录。pending 表示待人工检查。未匹配到结果或无法访问索引时直接说明。没有登记的数量、页数、风格和下载地址不得推测。

每条结果需包含资源名称、所属网盘合集、原始文件夹路径和网盘分享入口。合集内多个命中合并，多个合集分别列出。

统计口径见 manifest.json。资源索引项与已确认 PPT 文件数是不同指标。confirmed_ppt_count 来自已读取的目录元数据，null 代表暂无可确认的数据。
