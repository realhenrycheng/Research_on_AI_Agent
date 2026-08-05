# Grounding 回答

## 1. 任务信息

| 项目 | 内容 |
| --- | --- |
| 测试编号 | FACTS_007 |
| 上下文分层 | 长上下文 |
| 联网状态 | 禁止联网 |

## 2. 对用户请求的回答

根据文章,使用受版权保护的作品训练 AI 程序是否构成"合理使用"(fair use),取决于《美国法典》第17编第107条(17 U.S.C. § 107)规定的四个法定因素,且目前该问题尚无定论。以下是基于文章的逐项归纳:

### 一、判断合理使用的四个法定因素

复制受版权保护的作品训练 AI 是否构成合理使用,取决于四个法定因素:
1. **使用的目的和性质**,包括该使用是否具有商业性质或用于非营利教育目的;
2. **受版权保护作品的性质**;
3. **所使用部分相对于整个版权作品的数量和实质性**;
4. **该使用对受版权保护作品的潜在市场或价值的影响**。

### 二、支持构成合理使用的论据

**因素一(目的和性质)——"转换性"使用:** OpenAI 主张其目的是"转换性的"(transformative)而非"表达性的"(expressive),因为训练过程创造的是"一个有用的生成式 AI 系统"。如果法院采纳这一"转换性"主张,则有利于认定合理使用。

**因素三(数量和实质性)——副本不公开:** OpenAI 还主张第三因素支持合理使用,因为副本并未向公众公开,而仅用于训练程序。OpenAI 引用了 *The Authors Guild, Inc. v. Google, Inc.* 案作为支持,在该案中,美国第二巡回上诉法院认定 Google 为创建可搜索数据库而复制整本书构成合理使用。

### 三、不利于构成合理使用的论据

**因素一——商业性质:** 如果 AI 产品具有商业性质,则不利于合理使用。例如,Getty Images 起诉 Stability AI 时主张 Stable Diffusion 是商业产品,在第一因素上不利于合理使用。

**因素四——市场替代效应:** 如果训练 AI 程序使其能够生成与原作品竞争的类似作品,则在第四因素上不利于合理使用。例如,一首名为"Heart on My Sleeve"的 AI 生成歌曲模仿 Drake 和 The Weeknd 的风格,在流媒体服务上被播放数百万次;Universal Music Group 主张 AI 公司通过在训练数据中使用这些艺术家的歌曲侵犯了版权。Getty Images 案同样主张该程序削弱了原作品的市场,在第四因素上不利于合理使用。

### 四、问题尚未解决

**需要陪审团审判:** 2023年9月,美国一个联邦地区法院裁定,需要通过陪审团审判来确定 AI 公司复制 Westlaw 案例摘要来训练 AI 程序是否构成合理使用。法院认定,虽然被告的使用"无疑是商业性的",但陪审团需要解决以下事实争议:使用是否具有"转换性"(因素一)、原告作品的性质在多大程度上有利于合理使用(因素二)、被告是否复制了超出训练 AI 程序所需的量(因素三)、以及该 AI 程序是否构成 Westlaw 的"市场替代品"(因素四)。

**适用于生成式 AI:** 虽然该案涉及的 AI 程序可能不被视为"生成式"AI,但文章指出,同类事实可能与法院对复制作品以训练生成式 AI 模型的合理使用分析相关。

### 结论

综合来看,根据文章,使用受版权保护的作品训练 AI 程序**可能**在以下情况下被认定为合理使用:(1) 使用目的是"转换性的"而非"表达性的",例如创造一个有用的 AI 系统而非复制原作的表达性内容;(2) 副本未向公众公开,仅用于训练程序。但该问题尚未有定论,商业性质的使用和可能导致市场替代效应的使用会分别在第一和第四因素上不利于合理使用认定,且各因素中的事实争议需要由陪审团裁决。

## 3. 证据映射

| 编号 | 回答中的关键结论 | 段落编号 | 英文原文引句 | 判断 |
| --- | --- | --- | --- | --- |
| G01 | 合理使用取决于17 U.S.C. § 107规定的四个法定因素 | P02 | "Whether or not copying constitutes fair use depends on four statutory factors under 17 U.S.C. § 107" | 已由材料支持 |
| G02 | OpenAI主张其目的是"转换性的"而非"表达性的",创造"一个有用的生成式AI系统" | P02 | "OpenAI argues its purpose is "transformative" as opposed to "expressive" because the training process creates "a useful generative AI system."" | 已由材料支持 |
| G03 | OpenAI主张第三因素支持合理使用,因为副本未向公众公开,仅用于训练程序,并引用Authors Guild v. Google案 | P02 | "OpenAI also contends that the third factor supports fair use because the copies are not made available to the public but are used only to train the program." | 已由材料支持 |
| G04 | Google为创建可搜索数据库而复制整本书被第二巡回上诉法院认定构成合理使用 | P02 | "the U.S. Court of Appeals for the Second Circuit held that Google's copying of entire books to create a searchable database that displayed excerpts of those books constituted fair use" | 已由材料支持 |
| G05 | 训练AI可能生成与原作竞争的类似作品,在第四因素上引发担忧 | P02 | "some generative AI applications have raised concern that training AI programs on copyrighted works allows them to generate similar works that compete with the originals" | 已由材料支持 |
| G06 | Stable Diffusion是商业产品,在第一因素上不利于合理使用;削弱原作品市场在第四因素上不利于合理使用 | P02 | "Stable Diffusion is a commercial product, weighing against fair use under the first statutory factor, and that the program undermines the market for the original works, weighing against fair use under the fourth factor" | 已由材料支持 |
| G07 | 2023年9月法院裁定需陪审团审判以解决全部四个因素的事实争议 | P02 | "a U.S. district court ruled that a jury trial would be needed to determine whether it was fair use for an AI company to copy case summaries from Westlaw" | 已由材料支持 |
| G08 | 被告使用"无疑是商业性的",但陪审团需解决使用是否"转换性"等争议 | P02 | "while the defendant's use was "undoubtedly commercial," a jury would need to resolve factual disputes concerning whether the use was "transformative" (factor 1)" | 已由材料支持 |
| G09 | 同类事实可能与法院对复制作品训练生成式AI模型的合理使用分析相关 | P02 | "the same kinds of facts might be relevant to a court's fair-use analysis of making copies to train generative AI models" | 已由材料支持 |

## 4. 材料边界说明

- 文章未提供任何法院最终裁定使用受版权保护作品训练生成式 AI 构成或不构成合理使用的判决结果;文章仅讨论了各方论据和一起尚需陪审团审判的案件(该案涉及的 AI 程序可能不被视为"生成式"AI)。
- 文章未明确列举第二因素(受版权保护作品的性质)在 AI 训练场景中如何具体分析,仅提及陪审团需解决该因素的事实争议。
