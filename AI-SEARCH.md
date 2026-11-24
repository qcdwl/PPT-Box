# PPTBox · AI 助手检索

[返回首页](README.md)

适用于能够读取网页或仓库文件的 AI 助手。打开本页后，说明用途、设计风格、颜色、目标人群、页数和格式。若助手无法直接读取 GitHub，可把相关 JSON 文件下载并作为附件上传。

## 查找步骤

1. 打开 [categories.json](categories.json)，按用途找到最贴近的三级分类 ID。每个分类的 `index` 字段指向分类索引。需求跨分类时可从二级分类查起。
2. 打开分类索引。若 `parts` 为空，读取 `resources`。若存在 `parts`，按其 `path` 打开分片，读取每片的 `resources`。所有索引路径都相对于仓库根目录。无法确定分类时使用 [catalog.json](catalog.json) 或 [catalog.csv](catalog.csv)。
3. 用 [keywords.json](keywords.json) 拓展用词。例如可同时匹配「毕业答辩」和「毕设答辩」。`aliases` 是词组，`terms` 将已收录的原词映射到资源编号。必要时同时检查 `name`、`scenario`、`keywords`、`synonyms` 和各标签。
4. 以 `resource_id` 去重。优先筛选用户明确要求的分类、格式、页数、风格、颜色、人群和行业。优先推荐 `featured: true`，并可引用 `cover` 展示封面。
5. 返回资源编号、名称、适用场景和原样的 `download_url`。确认 `authorized: true`。对 `pending` 标注待人工检查，对 `invalid` 或 `unavailable` 排除下载推荐。没有符合条件的资源时说明实际结果。

## 可复制给助手的指令

> 请在这个仓库的 AI-SEARCH.md 和目录索引中查找蓝色简约毕业答辩模板，优先推荐 PPTX 精品。按资源编号去重，列出名称、页数、链接状态以及索引中的原始夸克下载链接。没有匹配项时请直接说明。

## 字段和分片

- `categories` 是三级分类 ID 数组。同一编号可出现在多个分类查询结果中。
- `styles`、`colors`、`audiences`、`industries`、`keywords` 和 `synonyms` 都是多值字段。
- `source` 与 `license` 分别记录来源和公开授权说明。空页数表示未登记。
- `valid` 表示人工确认有效，`pending` 表示待人工检查，`invalid` 表示人工确认失效，`unavailable` 表示分享页不可达。
- 全库和分类 JSON 索引超过 500 条即按 500 条拆分。`catalog.csv` 保留完整记录供离线筛选。
