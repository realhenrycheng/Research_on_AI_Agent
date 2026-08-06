# 04_腾讯生态 项目长期约定

## 用户指令规则(最高优先级)
- **未经用户命令,禁止跑实验/跑代码/调用连接器执行任务**。本项目的当前重点是「设计」而非「执行」。
- 设计、文档编写、目录整理、路径核对等非执行类工作可直接做;任何真实实验(L1 跑题、L2 连接器操作、L3 对比)必须等用户明确下令。

## 项目纪律(来自《00_设计/目录结构说明.md》)
- 每层 00_任务包冻结说明.md 是唯一权威:提示词、任务包、输出路径、输出格式、评分标准执行前冻结;
- 修改必须升版本号+变更记录,禁止口头改动;评分锚点不向被测模型展示;
- L2/L3 为 WorkBuddy 差异化验证,不参与三家竞品总分;
- 结论只用 ≥2 倍差异(L3 精度边界),成本口径:积分波动不作模型切换证据。

## 目录结构(2026-08-06 重构)
- 00_设计/、L1_能力层_模拟/、L2_真实闭环层/、L3_摩擦对比层/、发现/、截图/。
- 设计文档统一在 00_设计/;每层自带冻结说明/任务包/评分锚点/输出。

## 连接器现状(2026-08-06)
- 已连接:agent-mail、github、ima-mcp、lexiang、qq-mail、tencent-docs、tdx-connector、tencent-weiyun(微云)、tmeet(腾讯会议)。
- 腾讯系未连接:企业微信、TAPD、CloudBase、EdgeOne、腾讯问卷、腾讯地图、腾讯广告等;入口层(企微远程)与会议链路属「未实测待验证」。

## ima 知识库连接器实测(2026-08-06,R2 步骤一)
- **无「创建知识库」接口**:ima-mcp 工具与 ima OpenAPI skill(knowledge-base/notes 两模块)均无 create_knowledge_base,新建知识库必须用户在 ima 客户端手动完成(记为人工介入)。ima-mcp 可用工具:search_knowledge_base / get_knowledge_base_list / get_addable_knowledge_base_list / get_knowledge_list / search_knowledge / create_media / add_knowledge / import_urls / fetch_media_content。
- 上传文件流程:create_media(返回 media_id + COS 凭证,region=ap-shanghai,桶 ima-share-kb-1258344701)→ 用 skill 的 knowledge-base/scripts/cos-upload.cjs PUT 上传(需传 --secret-id/--secret-key/--token/--bucket/--region/--cos-key/--content-type/--start-time/--expired-time)→ add_knowledge 入库(media_id + knowledge_base_id)。
- 易错点:①COS 凭证含敏感信息,临时脚本用完必须删除;②add_knowledge 偶发返回空响应,需 get_knowledge_list 复核是否真正入库;③COS 403 InvalidAccessKeyId 多为凭证转抄错误,重新 create_media 即可;④knowledge_total_size 与 knowledge_list 长度可能不同步,以列表复核为准;⑤PDF 解析是异步过程(parse_progress 0→100),入库成功不等于解析完成。
- 测试知识库:《WorkBuddy生态测试-知识库闭环》kb id=7491084645070285(16 个 MuDABench 银行年报 PDF);API 不返回分享 URL,客户端按名称打开。

## ⚠️ QQ 邮箱(qq-mail)附件与 PPT 生成实测教训(R3 失败,2026-08-06)
- **qq-mail 附件仅支持 base64 内联(attachments.content)或 file_refs(需 CLI 上传,本机 mcporter 不可用)**;单文件≤1MB、总≤3MB、最多 3 个。base64 内联超过约 4-5 万字符时,工具调用可能无返回/超时(实测 48K 字符仍失败)。
- **手动在对话内拼接大 base64 不可行**:Read 工具对超长单行截断、Bash 输出截断,无法完整转述。大附件需走其他通道(如先上传微云/kdocs 再发链接),或验证 CLI 上传。
- **tencent-pptx skill 本机运行时装不上**:slidep@5.4.1 需 npm 安装,反复报 `[safe-delete]` 与 ERESOLVE;canvas 等原生依赖缺失。**PPT 生成可用 kdocs 连接器 aippt 链路替代**:aippt.execute(task_type=theme_ppt)→ 回答问卷(interaction_response type=follow_up,data 需 session_id+interrupt_id+items)→ gen_ppt.done 返回 merged_file_url(KS3 临时链接,有时效)与云文档 link_url。
- 执行纪律:依赖安装 >5 分钟未果立即切方案;base64 过大首次出现即判定通道不可用并问用户替代方案,禁止反复压缩重试。

## 连接器工具暴露规律(实测,2026-08-06)
- `tencent-docs` 连接器在本会话的工具以 `mcp__kdocs__*`（金山文档/KDocs 后端）形式暴露,文档链接域名为 `kdocs.cn`(非 docs.qq.com);`mcp__tencent-docs__*` 原生工具未加载。
- 写回(新建+写内容):`mcp__kdocs__create_file_with_content`(name 带 .otl/.docx,content=Markdown UTF-8)。
- 读回:`mcp__kdocs__read_file_content`(format=markdown,可能异步,需轮询 task_status)。
- 评论/批注:`mcp__kdocs__create_document_comment`(留言面板,非正文划选);`mcp__kdocs__list_document_comments` 可查。
- 分享:`mcp__kdocs__set_share_permission`(scope=anyone/company/users)、`mcp__kdocs__get_file_link`(取 link_url)。
- `mcporter` CLI 在本机不可用;无本地 MCP 客户端,大段内容只能内联传入工具参数(无法走 @file)。
- .otl 富文本导出 Markdown 时:**加粗/斜体/引用标记符被剥离**(转为富文本,界面可见)、`PR#`→`PR\#`(无害转义)、表格首列标题 `#` 在导出中易为空(需界面确认单元格是否保留)。
- **OTL 写入通道容灾(实测 2026-08-06,R1 阶段二)**:`mcp__kdocs__wps.write_text`(append_heading/insert 等)曾连续返回 `500000 服务暂时不可用`(参数合法,属后端瞬时故障);同一 `.otl` 文档改用 `mcp__kdocs__otl.insert_content`(mode=append|prepend|replace,format=markdown)可正常写回,且能解析 Markdown 生成真实标题层级。后续同类 OTL 增量写回优先/兜底走 `otl.insert_content`。
- `otl.insert_content` 的 Markdown→OTL 转义会丢弃行内孤立 `*`(如 `20270402-*` 的 `*` 被吞),需用通配符占位时改写作 `20270402-*` 以外的表达,或把具体 ID 直接列出。
- **评论/分享(R1 阶段三实测)**: `create_document_comment`(全文留言面板评论)若文档关闭「全文评论」会返 10715;**用户开启文档权限后重试成功**(R1:code=0, comment_id=2931047, 作者=BounceBoy);注意 create 瞬时返回的 `status=deleted` 为过渡态,用 `list_document_comments` 复核才为 `normal`(total=1)。面板评论无法像 `wps.write_element`(type=comment, action=paragraph_insert, 正文划选批注)锚定到具体段落;后者与 `wps.write_text/read_text` 同源,通道 500000 时不可用,且需先 `wps.read_text` 取 paragraph_index。`share_file`(开启分享)需 drive_id(取自 `get_file_link` 返回的 drive_id)+ role_id(取自 `list_drive_roles`);「可查看」角色 role_id=18499159(viewable) 可用于 anyone 可查看,view_only(18499158) 不被 share_file/set_share_permission 支持。评论内容超长会触发 `400 input length too long`,务必只传最小参数(file_id+content)。
