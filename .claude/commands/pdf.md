将指定的 Markdown 文档转换为 PDF（使用 XeLaTeX + 中文字体）。

## 执行步骤

1. **确定目标文档**：使用 `$ARGUMENTS` 指定的文件路径。如果未指定，查找 `docs/` 目录下最近修改的 `.md` 文件。

2. **确认 XeLaTeX 可用**：运行 `which xelatex` 确认已安装。如果未安装，提示用户执行 `brew install texlive`。

3. **转换为 PDF**：使用 pandoc 执行转换：
   ```
   pandoc <input>.md -o <output>.pdf --pdf-engine=xelatex -V mainfont="Heiti SC" -V CJKmainfont="Heiti SC" -V geometry:margin=2.5cm
   ```
   输出文件与源文件同目录、同名，扩展名改为 `.pdf`。

4. **打开预览**：使用 `open` 命令打开生成的 PDF 文件。

5. **报告结果**：向用户展示生成的 PDF 文件路径和文件大小。
