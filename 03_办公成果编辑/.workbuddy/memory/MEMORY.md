# 项目长期记忆 — 办公成果编辑测试

## 项目概述
- 本项目执行 SpreadsheetBench 2 基准测试中的"办公成果编辑"任务（测试三）
- 每个任务包（OEDIT_xxx）包含一个输入 Excel 文件和任务说明，要求审计修复后输出修订文件 + 变更说明

## 关键规则
- 输出路径模板：`F:\GitHub\AI_Agent\03_办公成果编辑\原始输出\{平台输出目录}\{测试编号}\`
- 平台输出目录：WorkBuddy输出 / ChatGPT_Work输出 / TRAE_Work输出
- 交付文件：`{测试编号}_修订后.xlsx` + `变更说明.md`（模板见提示词文件）
- 禁止修改原始输入文件、禁止访问 golden/参考答案
- 变更说明必须包含：任务信息、已完成修改、复核方式、未完成或异常

## 技术环境
- Python venv：`C:/Users/程浩然/.workbuddy/binaries/python/envs/default/Scripts/python.exe`
- openpyxl 已安装在该 venv 中
- 读取公式用 `data_only=False`，读取计算值用 `data_only=True`

## 常见 Excel 问题类型
1. **嵌入硬编码**：公式中嵌入常数而非单元格引用（如 `=F8-62.457`）
2. **跨表引用缺失**：部分列未遵循同行其他列的引用模式
3. **硬编码值替代公式**：单元格直接写数字而非公式
4. **AVERAGE 误用**：对输入值使用 AVERAGE 公式
5. **公式模式不一致**：同一行不同列使用不同计算逻辑
