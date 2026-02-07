使用 NotebookLM 为指定文档生成演示文稿（Slide Deck）。

## 执行步骤

1. **读取文档**：读取 `$ARGUMENTS` 指定的文档文件。如果未指定，查找 `docs/` 目录下最近修改的 `.md` 文件。

2. **读取元数据**：读取文档同目录下的 `meta.json`，获取目标受众、使用场景等信息，用于指导 slides 生成指令。重点关注：
   - `shared.presentation_guidance`：跨文档通用的演示指引（如术语通俗化规则）
   - 目标文件的 `presentation_guidance`：该文档特有的演示指引（如架构描述准确性要求）
   - `target_audience` 和 `tone`：受众和语气

3. **创建 NotebookLM Notebook**：以文档标题创建一个新的 notebook。

4. **添加 Source**：将文档全文作为 text source 添加到 notebook 中。注意去除 markdown 链接中的 URL（保留链接文字），因为 NotebookLM 无法访问这些链接。

5. **生成 Slide Deck**：调用 `generate_slide_deck`，根据文档内容和元数据生成定制化的 slides 生成指令。指令应包含：
   - 使用中文
   - 按文档的叙事逻辑展开
   - 适配目标受众的认知水平（基于 meta.json 中的 `target_audience`）
   - 突出关键数据和核心概念
   - 每页内容简洁有力，适合商务演示
   - 将 meta.json 中 `presentation_guidance` 的所有规则（术语通俗化、准确性要求等）转化为具体的生成指令

6. **报告结果**：向用户展示 notebook ID 和生成状态，提示用户前往 NotebookLM 查看和下载 slides。
