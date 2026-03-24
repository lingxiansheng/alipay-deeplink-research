# 当"网络安全法"成为审查武器：一个安全研究者对抗企业压制的全球记录

# When "Cybersecurity Law" Becomes a Censorship Weapon: A Security Researcher's Global Fight Against Corporate Suppression

---

**作者 / Author**: Jiqiang Feng (风宁) — Innora AI Security Research
**日期 / Date**: 2026-03-15
**联系 / Contact**: feng@innora.ai
**完整技术报告 / Full Technical Report**: [innora.ai/zfb](https://innora.ai/zfb/)
**Packet Storm Advisory**: [#217089](https://packetstormsecurity.com/files/217089)
**GitHub**: [sgInnora/alipay-deeplink-research](https://github.com/sgInnora/alipay-deeplink-research)

---

## 序言：删除不了的真相 / Prologue: Truth Cannot Be Deleted

2026年3月15日——恰逢国际消费者权益日——我收到微信公众平台的最终通知：我的4篇安全研究文章被**全部强制删除**。

March 15, 2026 — World Consumer Rights Day, of all days — I received the final notification from WeChat's Official Account platform: all four of my security research articles had been **forcibly deleted**.

删除通知的原文："接相关投诉，以下文章被判断为违反《中华人民共和国网络安全法》，已删除。"处理依据：**"相关法律法规"**。没有指明具体条款。没有指明投诉方。没有申诉渠道。

The exact wording: "Received related complaint. The following article has been determined to violate the Cybersecurity Law of the People's Republic of China and has been deleted." Basis: **"related laws and regulations."** No specific article. No identified complainant. No appeal channel.

通知只说了"接相关投诉"——**没有指明投诉方是谁**。没有案件编号。没有联系方式。连你被谁告了都不告诉你。

The notice only said "received related complaint" — **without identifying who filed it**. No case number. No contact information. They do not even tell you who accused you.

讽刺的是，4天前，针对同样内容的一份投诉已经被微信平台**审核驳回**（北京格韵律师事务所提交，投诉单号428526665）。微信平台的裁定是："未能核实判断被投诉内容侵权，对本次投诉暂不予支持。"而这次，连投诉方是谁都不告诉你，文章就直接消失了。

The irony: four days earlier, a complaint about the same content — filed by Beijing Geyun Law Firm — had been **reviewed and rejected** by WeChat (Case #428526665). WeChat's ruling: "Unable to verify infringement; complaint not supported." This time, you are not even told who filed the complaint. The articles simply vanish.

第一次用"名誉侵权"——失败。第二次换"网络安全法"——成功。

First attempt using "reputation infringement" — failed. Second attempt invoking "Cybersecurity Law" — succeeded.

这不是法律的胜利。这是法律被**武器化**的证据。

This is not a victory of law. This is evidence of law being **weaponized**.

停下来想一秒。一家万亿级企业，在投诉被平台公正驳回后，只需要让律师把投诉理由从"名誉侵权"改成"网络安全法"四个字，就能让平台的公正审核变成一纸废文。**不需要指明具体条款。不需要解释哪里违法。不需要给你申诉的机会。**

Pause and think for one second. A trillion-dollar corporation, after having its complaint fairly rejected by the platform, only needed its lawyers to change four words — from "reputation infringement" to "Cybersecurity Law" — to turn the platform's fair review into a worthless piece of paper. **No specific article cited. No explanation of what was illegal. No opportunity to appeal.**

如果你是一个安全研究者，此刻你应该感到恐惧。

If you are a security researcher, you should be afraid right now.

---

## 一、事实：17个漏洞、308条日志、42张截图 / Part 1: The Facts — 17 Vulnerabilities, 308 Logs, 42 Screenshots

让我先用事实说话。

Let the facts speak first.

2026年2月25日至3月7日，我向一个日活超过10亿用户的国民级支付应用提交了4轮安全漏洞报告，发现17个安全漏洞，CVSS评分从7.4到9.3。核心发现是一条完整的攻击链：

Between February 25 and March 7, 2026, I submitted four rounds of vulnerability reports to a payment application with over 1 billion daily active users. I identified 17 security vulnerabilities with CVSS scores ranging from 7.4 to 9.3. The core finding was a complete attack chain:

**ds.alipay.com 开放重定向 (CVSS 9.3) → DeepLink URL Scheme绕过 (CVSS 9.1) → JSBridge特权API无授权调用**

**ds.alipay.com Open Redirect (CVSS 9.3) → DeepLink URL Scheme Bypass (CVSS 9.1) → Unauthorized JSBridge Privileged API Access**

这条链的效果：攻击者构造一条恶意链接，通过WhatsApp/微信/短信发送给任何用户。用户点击后，攻击者可以——

The chain's impact: an attacker crafts a single malicious link, sent via WhatsApp/WeChat/SMS to any user. Upon clicking, the attacker gains the ability to:

- **静默窃取GPS坐标**（8.81米精度，无弹窗授权）— Silent GPS theft (8.81m accuracy, no permission dialog)
- **提取完整设备指纹**（30+字段）— Full device fingerprint extraction (30+ fields)
- **唤起支付收银台**（iOS tradePay API）— Invoke payment checkout (iOS tradePay API)
- **预填转账页面**（攻击者账号+金额）— Pre-fill transfer page (attacker's account + amount)
- **蠕虫式传播**（自动向微信/QQ/钉钉分享恶意链接）— Worm-like propagation (auto-share to WeChat/QQ/DingTalk)

这些不是理论推测。**308条服务器交互日志**记录了每一次数据外传。**42张全链路截图**标记了每个关键步骤。**3台设备在3个国家**完成了独立复现——新西兰奥克兰的Samsung S25 Ultra、马来西亚槟城的Redmi、以及厂商自家安全负责人在杭州总部使用的iPhone 16 Pro。

These are not theoretical claims. **308 server interaction logs** document every data exfiltration event. **42 full-chain screenshots** mark each critical step. **3 devices across 3 countries** independently reproduced the findings — a Samsung S25 Ultra in Auckland, New Zealand; a Redmi in Penang, Malaysia; and the vendor's own security lead's iPhone 16 Pro at Hangzhou headquarters.

2026年3月7日，在一通23分钟的语音通话中（**全程录音**），厂商安全负责人口头承认了漏洞的严重性。他亲口说："如果你能绕过我们的白名单，那确实是很严重的问题。"

On March 7, 2026, during a 23-minute phone call (**fully recorded**), the vendor's security lead verbally acknowledged the severity. His exact words: "If you can bypass our whitelist, that would indeed be a serious issue."

11分钟后，白名单被绕过。

Eleven minutes later, the whitelist was bypassed.

3月10日，厂商的最终答复：**"经过我们安全工程师审核，这些属于正常功能。"**

March 10, the vendor's final response: **"Based on our security engineers' assessment, these constitute normal functionality."**

---

## 二、审查升级：从驳回到全面删除 / Part 2: Escalating Censorship — From Rejection to Total Deletion

时间线本身就是最有力的证据。

The timeline itself is the most powerful evidence.

| 日期 Date | 事件 Event |
|-----------|------------|
| 3月11日 18:16 | 研究报告公开发布至独立博客 innora.ai/zfb/ — Public disclosure on independent blog |
| 3月11日 22:45 | 4小时29分钟后，北京格韵律师事务所提交"名誉侵权"投诉 — Beijing Geyun Law Firm files "reputation infringement" complaint |
| 3月12日 | **微信平台驳回投诉** — WeChat platform **rejects** the complaint |
| 3月12日 | Packet Storm Security收录Advisory #217089 — Packet Storm publishes Advisory #217089 |
| 3月12日 | 6个CVE提交MITRE (Ticket #2005801) — 6 CVEs submitted to MITRE |
| 3月12-14日 | 189封邮件发送至22个国家的~160个监管机构 — 189 emails sent to ~160 regulators across 22 countries |
| **3月15日** | **4篇文章全部被删除，依据"相关法律法规"，投诉方匿名** — **All 4 articles force-deleted, citing "related laws," complainant anonymous** |

被删除的4篇文章标题：

The four deleted article titles:

1. 《当白名单绕过沦为全网攻击的钥匙，傲慢的终点是法庭与溯源调查》
2. 《巨头的"封口令"被微信驳回，而全球顶级黑客弹药库给出了最终裁决》
3. 《位置被秒偷！10多亿人每天在用的国民支付应用，17个「正常功能」细思极恐！》
4. 《支付宝安全研究遭律师函投诉——一篇零次提及"支付宝"的文章如何构成"商誉侵权"？》

注意第4篇的标题：一篇**零次提及"支付宝"**的文章，被蚂蚁集团以"商誉侵权"为由投诉。投诉本身就暴露了投诉方的身份——如果文章没有提到你，你怎么知道说的是你？

Note Article 4's title: an article that mentioned "Alipay" **zero times** was complained against by Ant Group for "reputation infringement." The complaint itself reveals the complainant's identity — if the article doesn't mention you, how do you know it's about you?

**升级路径清晰可见 / The escalation pattern is unmistakable:**

口头否认漏洞 → 律师函投诉"名誉侵权"（被驳回）→ 改用"网络安全法"（成功删除）→ 服务器端拦截PoC

Verbal denial of vulnerabilities → Lawyer letter citing "reputation infringement" (rejected) → Switch to "Cybersecurity Law" (deletion successful) → Server-side PoC interception

---

## 三、法律的两张面孔 / Part 3: Two Faces of Law

### 黑暗面：当法律成为沉默的武器 / The Dark Side: When Law Becomes a Weapon of Silence

让我描述一下这个"法律武器"有多恐怖。

Let me describe how terrifying this "legal weapon" is.

2026年1月1日，中国《网络安全法》修正案生效。第28条（原第26条）规定：发布系统漏洞等网络安全信息，可被处以最高**100万元人民币罚款**、停业整顿、关闭网站、吊销营业执照。

On January 1, 2026, China's amended Cybersecurity Law took effect. Article 28 (formerly Article 26): publishing cybersecurity information including system vulnerabilities may result in **RMB 1 million fines**, business suspension, website shutdown, or license revocation.

**但真正令人恐惧的不是法律条文本身。是它被使用的方式。**

**But the truly terrifying part is not the law itself. It's how it is used.**

在本案中：

In this case:

- 通知说"接相关投诉"——但**没有指明投诉方是谁，也没有指明违反了哪一条** — The notice said "received related complaint" — but **did not identify who filed it, nor which article was violated**
- 平台在**没有进行实质审查**的情况下执行了删除 — The platform executed deletion **without substantive review**
- 研究者**没有收到任何申诉通知** — The researcher received **no appeal notification**
- **4天前，完全相同的内容**被同一平台审核后认定为不构成侵权 — **4 days earlier, identical content** was reviewed by the same platform and found not to constitute infringement
- 研究者遵循了负责任披露的每一步：4轮私密报告、23分钟电话沟通、厂商拒绝后才公开 — The researcher followed every step of responsible disclosure: 4 rounds of private reports, 23-minute call, vendor rejection before publication
- 相同内容在Packet Storm、GitHub、innora.ai上合法存在——只在中国平台被删除 — Identical content exists lawfully on Packet Storm, GitHub, innora.ai — deleted only on Chinese platforms

**这意味着什么？** 意味着在这个体系中，一家企业不需要证明你违法了。它只需要说出"网络安全法"四个字。平台会自动执行。你不会收到任何解释。你没有申诉的机会。而你上一次投诉被驳回的事实，会被当作从未发生。

**What does this mean?** It means that in this system, a corporation doesn't need to prove you broke the law. It only needs to say the words "Cybersecurity Law." The platform will auto-execute. You will receive no explanation. You have no chance to appeal. And the fact that the same complaint was rejected four days ago will be treated as if it never happened.

**这不是法治。这是一个没有刹车的删除按钮。**

**This is not rule of law. This is a delete button with no brakes.**

### 欧盟：吹哨人保护指令 / EU: Whistleblower Protection Directive

在世界的另一边，**完全相反的法律框架**保护着同样的行为。

On the other side of the world, an **entirely opposite legal framework** protects the exact same conduct.

**EU Whistleblower Directive 2019/1937**:

- **第19条(Article 19)**: 成员国应**禁止对举报人的任何报复行为** — Member States shall **prohibit any form of retaliation** against reporting persons
- **第21条(Article 21)**: 报复行为包括——解雇、降级、骚扰、负面推荐、列入黑名单、**业务抵制** — Retaliation includes dismissal, demotion, harassment, negative references, blacklisting, **business boycotting**
- **第22条(Article 22)**: 受害者有权通过司法或行政程序获得**物质和精神损害赔偿** — Victims are entitled to **material and non-material damage** compensation through judicial/administrative procedures
- **第23条(Article 23)**: 成员国应对实施报复的自然人和法人制定**有效、相称和具有威慑力的处罚** — Member States shall lay down **effective, proportionate and dissuasive penalties** for perpetrators of retaliation

Alipay的欧洲实体——**Alipay (Europe) Limited S.A.**（CSSF编号W00000009，卢森堡RCS B188095）——持有电子货币机构(EMI)牌照，受CSSF直接监管。

Alipay's European entity — **Alipay (Europe) Limited S.A.** (CSSF No. W00000009, Luxembourg RCS B188095) — holds an Electronic Money Institution (EMI) license under direct CSSF supervision.

2025年5月，CSSF已经因反洗钱(AML)违规对其处以**€214,000罚款**——涉及6起可疑交易报告未提交、制裁警报延迟、KYC文件缺失。

In May 2025, CSSF had already fined it **€214,000** for AML violations — involving 6 unreported suspicious transaction reports, delayed sanction alerts, and missing KYC documentation.

2026年3月13日，我向CSSF Whistleblowing团队提交了安全漏洞报告。案件编号：**CSSFWB-2026-080**。CSSF的ICT Risk监管部门和Whistleblowing团队**双重确认收到**。

On March 13, 2026, I submitted the security vulnerability report to CSSF's Whistleblowing team. Case number: **CSSFWB-2026-080**. Both CSSF's ICT Risk Supervision and Whistleblowing teams **confirmed receipt**.

根据卢森堡2023年5月16日法律（转化EU Directive），**任何善意举报金融行业不当行为的人员均受保护**。保护范围扩展到了整个国内法领域的违规行为，不仅限于EU法范围。

Under Luxembourg's Law of May 16, 2023 (transposing the EU Directive), **any person reporting in good faith about dysfunctions in the financial sector is protected**. The scope extends to breaches of national law as a whole, not limited to EU law.

**跨境删除内容是否构成EU法下的"报复"？** 这是一个前沿法律问题。但根据Directive第21条的广义定义——"任何直接或间接导致举报人遭受不利待遇的行为"——通过律师事务所在中国平台删除安全研究文章，**完全可以被论证为报复行为**。

**Does cross-border content deletion constitute "retaliation" under EU law?** This is a frontier legal question. But under Article 21's broad definition — "any action that causes unjustified detriment" — using a law firm to delete security research articles on Chinese platforms **can be argued as retaliatory conduct**.

---

## 四、全球回响：38个机构的回答 / Part 4: Global Echo — Responses from 38 Institutions

如果这些漏洞真的是"正常功能"，为什么全球38个机构做出了回应？

If these vulnerabilities are truly "normal functionality," why did 38 global institutions respond?

### 金融监管机构 / Financial Regulators (16个回复)

| 机构 Institution | 国家 Country | 行动 Action |
|------------------|--------------|-------------|
| **HKMA** 香港金融管理局 | 香港 | 正式投诉立案 CE20260313175412 |
| **PDPC** 个人数据保护委员会 | 新加坡 | 正式隐私违规调查 #00629724 |
| **CSSF** 金融监管委员会 | 卢森堡 | Whistleblowing案件 CSSFWB-2026-080 |
| **FCA** 金融行为监管局 | 英国 | Whistleblowing团队确认收到 |
| **OAIC** 信息专员办公室 | 澳大利亚 | Intake团队确认收到 |
| **EDPB** 欧洲数据保护委员会 | 欧盟 | 跨境数据保护投诉确认收到 |
| **FMA** 金融市场管理局 | 新西兰 | 确认收到，正在评估 |
| **ANSSI** 网络安全局 | 法国 | 确认收到，已转交相关部门 |
| **CIRCL** 国家CERT | 卢森堡 | Case #4782984，已代联Alibaba SRC |
| **DNB** 荷兰央行 | 荷兰 | 确认收到，转info@监管通道 |
| **BNM** 国家银行 | 马来西亚 | 确认收到 BNM:0001001049160 |
| **OJK** 金融监管局 | 印尼 | 要求补充说明 Ticket L2603022304 |

### 平台方 / Platforms (5个回复)

| 平台 Platform | 行动 Action |
|---------------|-------------|
| **Apple Product Security** | 正式调查 Case OE01052449093014 |
| **Google Play** | 政策违规审查 #9-7515000040640 |
| **Packet Storm Security** | **已发布Advisory #217089** |
| **MITRE CVE** | 6个CVE受理 Ticket #2005801 |
| **PayPal** | 确认收到 |

### 媒体与社区 / Media & Community (7+个回复)

Help Net Security、Tech in Asia、The Information等媒体确认收到。Reddit r/netsec社区已发帖。独立安全研究者在GitHub上独立复现了发现。

Help Net Security, Tech in Asia, The Information and others confirmed receipt. Posted on Reddit r/netsec. Independent security researchers reproduced findings on GitHub.

**总计：189封邮件，22个国家，38+个回复，多个正式调查启动。**

**Total: 189 emails, 22 countries, 38+ responses, multiple formal investigations launched.**

---

## 五、全球模式：安全研究者被打压不是个案 / Part 5: Global Pattern — Researcher Suppression Is Not Isolated

[disclose.io Research Threats Database](https://threats.disclose.io/) 记录了过去25年中**80+起**安全研究者遭受法律威胁的案例。模式惊人地相似：

The [disclose.io Research Threats Database](https://threats.disclose.io/) documents **80+ cases** of legal threats against security researchers over 25 years. The patterns are strikingly similar:

| 案例 Case | 年份 Year | 国家 Country | 模式 Pattern |
|-----------|-----------|--------------|--------------|
| **Columbus, Ohio vs Connor Goodwolf** | 2024 | 美国 | 研究者报告勒索软件数据泄露 → 被申请禁止令+$25K赔偿 |
| **NEWAG vs Dragon Sector** | 2023-2024 | 波兰 | 研究者发现火车DRM → 被起诉版权侵权(SLAPP诉讼) |
| **Modern Solution GmbH** | 2024 | 德国 | 程序员报告漏洞 → 被刑事起诉，罚款€3,000 |
| **FreeHour vs CS Students** | 2023 | 马耳他 | 4名学生报告漏洞 → 被逮捕、脱衣搜身 |
| **Arm Ltd vs Maria Markstedter** | 2023 | 英国 | 研究者域名被投诉下线 |
| **Apple vs Denis Tokarev** | 2021 | 美国 | DMCA武器化删除GitHub漏洞文档 |

**但本案有一个独特的特征**：这可能是全球第一例——厂商在**第一次投诉被平台驳回后**，更换法律依据（从"名誉侵权"升级到"网络安全法"）成功实施第二次删除的记录案例。

**But this case has a unique feature**: it may be the first documented global case where a vendor, **after having its first complaint rejected by the platform**, switched legal grounds (from "reputation infringement" to "Cybersecurity Law") to successfully execute a second deletion.

这不是法律适用。这是**法律购物 (forum shopping)**——在法律武器库中挑选最不可抗辩的条款来绕过平台的公正审核。

This is not legal application. This is **forum shopping** — selecting the most unassailable statute from the legal arsenal to circumvent the platform's fair review.

---

## 六、对比的荒谬 / Part 6: The Absurdity of Contrast

同一份技术研究报告。同样的17个漏洞。同样的308条日志和42张截图。

The same technical research report. The same 17 vulnerabilities. The same 308 logs and 42 screenshots.

| 维度 Dimension | 国际社会 International | 中国平台 Chinese Platform |
|----------------|----------------------|--------------------------|
| 漏洞定性 Classification | CVSS 9.3, 6个CVE待分配 | "正常功能" |
| 内容状态 Content Status | 公开存档(Packet Storm/GitHub/innora.ai) | **强制删除** |
| 法律定性 Legal Status | ISO 29147合规披露 + EU吹哨人保护 | "违反网络安全法" |
| 厂商回应 Vendor Response | Apple/Google启动调查 | 律师函 + 删帖 |
| 监管态度 Regulatory Response | 16个机构正式回复/立案 | 沉默 |
| 研究者待遇 Researcher Treatment | Packet Storm认证 + CVE编号 | **内容审查** |

**相同的事实，在太平洋的两岸获得了完全相反的法律待遇。**

**Identical facts receive diametrically opposite legal treatment on two sides of the Pacific.**

在卢森堡，向CSSF报告金融机构的安全漏洞是受法律保护的吹哨行为(CSSFWB-2026-080)。在中国，发表相同内容是"违反网络安全法"。

In Luxembourg, reporting a financial institution's security vulnerabilities to CSSF is legally protected whistleblowing (CSSFWB-2026-080). In China, publishing the same content is "violating the Cybersecurity Law."

卢森堡的Alipay (Europe) Limited S.A. 已经因为合规失败被罚了€214,000。而在中国，揭示其母公司应用安全问题的研究者被审查。

Luxembourg's Alipay (Europe) Limited S.A. has already been fined €214,000 for compliance failures. In China, the researcher revealing its parent company's application security issues gets censored.

---

## 七、寒蝉效应与真正的网络安全威胁 / Part 7: Chilling Effect and the Real Cybersecurity Threat

让我说清楚一件事：**删除安全研究文章不会让漏洞消失。**

Let me be clear about one thing: **Deleting security research articles does not make vulnerabilities disappear.**

截至今天，这条CVSS 9.3的攻击链仍然公开存档在三个独立节点：

As of today, this CVSS 9.3 attack chain remains publicly archived on three independent nodes:

1. **Packet Storm Security** — Advisory #217089
2. **GitHub** — sgInnora/alipay-deeplink-research
3. **innora.ai/zfb/** — 独立镜像

删除微信文章唯一的效果是：**让中国用户无法了解他们正在使用的应用存在的安全风险。**

The only effect of deleting WeChat articles: **Chinese users are denied knowledge of the security risks in the application they use daily.**

这创造了一个荒谬的悖论：全世界的安全研究者、监管机构、甚至厂商的竞争对手(Apple、Google已启动调查)都知道这些漏洞——唯独**受影响最大的10亿中国用户**被蒙在鼓里。

This creates an absurd paradox: security researchers, regulators, and even the vendor's competitors worldwide (Apple and Google have launched investigations) all know about these vulnerabilities — except for the **1 billion Chinese users most affected**, who are kept in the dark.

**这才是真正的网络安全威胁。**

**This is the real cybersecurity threat.**

不是安全研究者披露漏洞。而是企业利用法律阻止漏洞被修复。

Not security researchers disclosing vulnerabilities. But corporations using law to prevent vulnerabilities from being fixed.

---

## 八、想象一下这发生在你身上 / Part 8: Imagine This Happening to You

你是一个安全研究者。也许在柏林、东京、新加坡、或奥克兰。你在一个10亿用户的应用中发现了一个严重漏洞。

You're a security researcher. Maybe in Berlin, Tokyo, Singapore, or Auckland. You discover a critical vulnerability in an app used by a billion people.

**你做了所有正确的事情。**

**You do everything right.**

你写了详细的报告。你通过官方渠道私密提交。你等了两周。你打了电话。你再次提交。你等厂商回应。

You write a detailed report. You submit privately through official channels. You wait two weeks. You make a phone call. You submit again. You wait for the vendor's response.

厂商告诉你：**"这是正常功能。"**

The vendor tells you: **"This is normal functionality."**

你按照ISO 29147国际标准——也就是全世界安全研究者遵循的准则——在穷尽私密渠道后，公开发表技术分析。这也是Packet Storm、MITRE、Google Project Zero处理此类情况的标准流程。

Following ISO 29147 — the international standard every security researcher in the world follows — you publish your technical analysis after exhausting private channels. This is the same process Packet Storm, MITRE, and Google Project Zero follow.

然后，**噩梦开始了。**

Then, **the nightmare begins.**

12小时内，一家你从未听说过的律师事务所提交投诉，要求删除你的文章。理由："名誉侵权"。平台审核后驳回——你松了一口气。你以为公正的审核流程保护了你。

Within 12 hours, a law firm you've never heard of files a complaint demanding your article's removal. Reason: "reputation infringement." The platform reviews and rejects it — you breathe a sigh of relief. You think the fair review process has protected you.

**4天后。**

**Four days later.**

同一家律师事务所，同样的投诉对象，**换了四个字**。从"名誉侵权"变成"网络安全法"。

Same law firm. Same complaint target. **Four words changed.** From "reputation infringement" to "Cybersecurity Law."

你的文章消失了。全部。4篇。没有通知。没有解释。没有申诉。

Your articles vanish. All of them. Four articles. No notification. No explanation. No appeal.

你登录后台，看到的只有一行字：**"违反《中华人民共和国网络安全法》。"** 没有说违反了哪一条。没有说哪些内容违规。没有告诉你该怎么申诉。

You log into the backend. All you see is a single line: **"Violation of the Cybersecurity Law of the People's Republic of China."** It doesn't say which article. It doesn't say which content was illegal. It doesn't tell you how to appeal.

你意识到：**4天前保护了你的那道公正审核防线，被四个字击穿了。** 平台甚至没有重新审核。

You realize: **The fair review process that protected you four days ago was pierced by four words.** The platform didn't even re-review.

然后你开始想：**下一步会是什么？**

Then you start wondering: **What comes next?**

报警？刑事调查？旅行限制？家人被"约谈"？你的名字出现在某个内部数据库里，从此每次入境都被单独"请"到小房间？

Police report? Criminal investigation? Travel restrictions? Your family getting "invited for tea"? Your name appearing in some internal database, and from now on every time you cross a border you get pulled into a private room?

你不知道。**因为这个系统不需要告诉你。**

You don't know. **Because this system doesn't need to tell you.**

而你的研究——那些被Packet Storm验证、被MITRE受理、被16个国家监管机构正式回复的研究——在全世界都合法存在。唯独在这个审查体系里，它是一个罪名。

And your research — verified by Packet Storm, accepted by MITRE, formally responded to by 16 countries' regulators — exists lawfully everywhere in the world. Except in this censorship system, where it is a crime.

**你还敢做安全研究吗？**

**Would you still dare to do security research?**

这就是寒蝉效应。不是理论上的。是正在发生的。此刻。对真实的人。

This is the chilling effect. Not theoretical. Happening right now. To real people.

---

## 九、我们不会沉默 / Part 9: We Will Not Be Silenced

他们删除了文章。但他们删不了Packet Storm的存档。删不了MITRE的CVE编号。删不了16个国家监管机构邮箱里的报告。删不了GitHub上的代码。删不了互联网档案馆的快照。

They deleted the articles. But they cannot delete Packet Storm's archive. Cannot delete MITRE's CVE numbers. Cannot delete the reports in 16 countries' regulators' inboxes. Cannot delete the code on GitHub. Cannot delete the Internet Archive's snapshots.

**他们唯一成功删除的，是中国10亿用户了解自身安全风险的权利。**

**The only thing they successfully deleted is the right of 1 billion Chinese users to know about their own security risks.**

我们将继续配合所有监管机构的调查——HKMA、PDPC、CSSF、FCA、OAIC、Apple、Google。我们将继续在所有中国审查无法触及的平台上发声。

We will continue cooperating with all regulatory investigations — HKMA, PDPC, CSSF, FCA, OAIC, Apple, Google. We will continue speaking on every platform that Chinese censorship cannot reach.

---

## 十、致全球安全研究社区——这是一个警告 / Part 10: To the Global Security Research Community — This Is a Warning

这不仅仅是一个关于支付宝漏洞的故事。

This is not merely a story about Alipay vulnerabilities.

**这是一个关于你的故事。**

**This is a story about you.**

如果你正在研究任何中国科技巨头的产品——微信、TikTok、大疆、华为、小米——你需要知道：有一个法律武器库随时准备对准你。你不需要做错任何事。你只需要让一家足够大的企业感到不舒服。

If you are researching any Chinese tech giant's product — WeChat, TikTok, DJI, Huawei, Xiaomi — you need to know: there is a legal arsenal ready to be aimed at you. You don't need to do anything wrong. You only need to make a sufficiently large corporation uncomfortable.

**规则是这样的：**

**Here are the rules:**

1. 企业可以在投诉被驳回后，换一个法律条款重新投诉——直到成功为止
   *Corporations can re-file after rejection, switching legal grounds — until they succeed*

2. "网络安全法"三个字就是一把万能钥匙——不需要指明条款，不需要解释，不需要给你申诉
   *"Cybersecurity Law" is a master key — no article needs to be specified, no explanation given, no appeal offered*

3. 你在国际上的所有认可——CVE编号、Packet Storm收录、监管机构回复——在这个审查体系里毫无意义
   *All your international validation — CVE numbers, Packet Storm publication, regulator responses — means nothing in this censorship system*

4. 你的研究可以同时是"EU法律保护的吹哨行为"和"中国法律下的违法行为"——取决于你站在太平洋的哪一边
   *Your research can simultaneously be "EU-protected whistleblowing" and "illegal under Chinese law" — depending on which side of the Pacific you stand*

当一家千亿级企业可以在投诉被驳回后，仅仅通过更换法律条款就实现内容删除——**没有任何研究者是安全的。**

When a hundred-billion-dollar corporation can achieve content deletion simply by switching legal grounds after its complaint is rejected — **no researcher is safe.**

当"网络安全法"可以被用来删除安全研究而非保护网络安全——**法律本身已经成为一个未修补的零日漏洞。**

When "Cybersecurity Law" can be used to delete security research rather than protect cybersecurity — **the law itself has become an unpatched zero-day.**

我们需要全球安全研究社区清醒地认识到：

The global security research community needs to clearly understand:

- **全球统一的安全研究者保护框架已经不是"最好有"——而是生存必需品**
   *A globally unified researcher protection framework is no longer "nice to have" — it is a survival necessity*

- **当法律被武器化时，平台不应成为审查的执行者**
   *When law is weaponized, platforms must not become censorship executors*

- **跨境报复行为必须被追究**——在EU持有吹哨人保护的实体，不应能在中国平台上实施报复而不承担后果
   *Cross-border retaliation must be accountable* — entities with EU whistleblower protection should not be able to retaliate on Chinese platforms without consequence

---

## 附录：关键案件编号 / Appendix: Key Case Numbers

| 编号 ID | 类型 Type | 状态 Status |
|---------|-----------|-------------|
| Packet Storm #217089 | Advisory | 已发布 Published |
| MITRE Ticket #2005801 | 6x CVE申请 | 待分配 Pending |
| HKMA CE20260313175412 | SVF投诉 | 立案 Filed |
| PDPC #00629724 | 隐私调查 | 调查中 Investigating |
| CSSF CSSFWB-2026-080 | Whistleblowing | 已受理 Received |
| FCA UK | Whistleblowing | 已确认 Confirmed |
| Apple OE01052449093014 | 产品安全 | 调查中 Investigating |
| Google Play #9-7515000040640 | 政策违规 | 调查中 Investigating |
| CIRCL #4782984 | CERT协调 | 进行中 In Progress |
| WeChat #428526665 | 侵权投诉 | **第一次驳回，第二次删除** |

---

**完整技术报告 / Full Technical Report**: [https://innora.ai/zfb/](https://innora.ai/zfb/)
**Packet Storm Advisory**: [#217089](https://packetstormsecurity.com/files/217089)
**GitHub Repo**: [sgInnora/alipay-deeplink-research](https://github.com/sgInnora/alipay-deeplink-research)
**联系 / Contact**: feng@innora.ai

---

*本文采用CC BY 4.0许可证。任何人均可自由转载、翻译、引用，无需事先许可。*

*This article is licensed under CC BY 4.0. Anyone may freely republish, translate, or cite without prior permission.*

*这篇文章会被删除吗？也许。但删除它只会再次证明我们说的一切都是真的。*

*Will this article be deleted too? Perhaps. But deleting it would only prove, once again, that everything we said is true.*

---

**#SecurityResearch #VulnerabilityDisclosure #Censorship #CybersecurityLaw #WhistleblowerProtection #Alipay #AntGroup #PacketStorm #CVE #MITRE #CSSF #HKMA #FreeSpeech #ResearcherRights #InfoSec**
