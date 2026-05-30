---
name: physics-summer-camp-monitor-pack
description: Use when searching, collecting, and packaging recent Chinese physics-related summer-camp, pre-admission, 推免, or graduate-application notices for self-media publishing. Focus on official notices, application deadlines, required materials, eligibility, assessment format, source links, and publish-ready reminder copy.
---

# 物理保研夏令营信息抓取

## 统一输出目录

所有本 skill 生成的内容，统一放在用户工作区：

```text
skill-outputs/03-physics-summer-camp-monitor-pack/
```

每一次输出必须单独建一个小文件夹，文件夹名要能直接看出“日期 + 查询范围 + 主题 + 内容类型”：

```text
YYYY-MM-DD-date-range-topic-camp-monitor/
```

示例：

```text
skill-outputs/03-physics-summer-camp-monitor-pack/2026-05-30-2026-05-24-to-2026-05-30-physics-camps-monitor/
skill-outputs/03-physics-summer-camp-monitor-pack/2026-06-06-2026-05-31-to-2026-06-06-optics-physics-camps-monitor/
```

不要把正式产物散放在 `summer-camp-packs/` 根目录；`summer-camp-packs/` 只作为旧产物或临时草稿目录。

这个 skill 用来做“最近开放的物理相关夏令营/推免/预报名信息”抓取和自媒体提醒包。

重点不是泛泛介绍学校，而是回答：

```text
最近有哪些物理相关夏令营开放了？
什么时候截止？
要准备哪些材料？
报名入口在哪里？
考核形式是什么？
适合什么背景的同学关注？
```

## 适用场景

- 查询最近一周物理相关夏令营通知；
- 整理某批院校夏令营开放信息；
- 做小红书/公众号“本周物理保研夏令营更新”；
- 提醒读者准备申请材料和截止时间；
- 给后续“院校方向介绍”内容提供选题来源。

## 信息来源规则

优先级：

1. 学院/系官网通知公告；
2. 学校研究生招生网；
3. 学校教务/本科生院/研究生院通知；
4. 官方公众号文章，仅作补充；
5. 第三方汇总只能作为线索，不能作为最终来源。

必须标注官方链接。没有官方链接的通知，不进入正式表格，只能放入“待核验线索”。

## 链接与考核形式校验

正式输出前必须做三项校验：

1. `official-links.csv` 里的每个 URL 必须能在本次任务中打开或成功抓取。
2. 截止时间、材料清单、考核/选拔形式必须来自官方通知；如果通知未明确，就写“通知未明确”。
3. 如果是历史通知，必须写清具体入学年份或通知年份，例如“2026 入学推免通知”“2023 统考复试细则”。

不要把“项目介绍页”当成招生通知；项目介绍页只能说明项目方向和导师线索，不能替代报名截止、材料、考核方式。

中文 CSV 必须使用 UTF-8 BOM。面向 Excel 查看时，重要表格建议同时输出 `.xlsx`。

## 输出文件夹

创建：

```text
summer-camp-packs/YYYY-MM-DD-physics-camp-weekly/
├─ source/
│  ├─ official-links.csv
│  ├─ search-log.md
│  └─ unverified-leads.csv
├─ camps.csv
├─ deadline-calendar.csv
├─ materials-checklist.md
├─ brief.md
├─ cards/
│  ├─ 01-cover.md
│  ├─ 02-deadline-table.md
│  ├─ 03-materials.md
│  ├─ 04-who-should-apply.md
│  ├─ 05-application-tips.md
│  └─ 06-risk-reminder.md
├─ publish.md
└─ checks.md
```

## 固定字段

`camps.csv` 必须包含：

```text
学校,院系/项目,通知标题,通知日期,报名截止时间,活动时间,报名入口,申请材料,考核/选拔形式,适合背景,官方链接,状态,备注
```

`deadline-calendar.csv` 必须包含：

```text
日期,学校,院系/项目,事项,官方链接,提醒文案
```

`official-links.csv` 必须包含：

```text
学校,院系/项目,通知标题,官方链接,发布日期,抓取日期,来源类型
```

## 查询范围

默认查询“最近 7 天”，但必须使用实际日期。

例：如果当前日期是 2026-05-30，查询范围写成：

```text
2026-05-24 至 2026-05-30
```

不要只写“最近一周”。

## 搜索关键词

组合搜索：

```text
物理 夏令营 优秀大学生 2026
物理学院 夏令营 报名通知
物理学系 全国优秀大学生夏令营
物理 推免 预报名 夏令营
物理 申请材料 截止时间 夏令营
```

如果用户指定方向，加入方向词：

```text
凝聚态 光学 量子 天文 粒子 电子科学 材料物理
```

## 提取重点

每条通知优先提取：

1. 报名截止时间
2. 申请材料
3. 报名入口/系统
4. 活动时间
5. 活动形式：线上/线下/现场/远程
6. 选拔或考核形式：面试、笔试、讲座、营员考核、综合考核
7. 申请资格：年级、专业、成绩排名、英语要求
8. 是否和推免预选拔相关

如果通知没有明确写某项，填“通知未明确”，不要猜。

## 自媒体文案规则

标题默认格式：

```text
27物理保研夏令营信息更新｜<日期范围>
```

正文必须突出：

- 哪些学校/院系新增通知；
- 申请截止时间；
- 需要准备的材料；
- 哪些通知和推免预选拔相关；
- 哪些信息需要读者自己再点官网核验。

写法示例：

```text
这周物理相关夏令营更新里，最需要先看的不是学校名字，而是截止时间。

建议先按“截止时间”排序，再看自己材料是否来得及补。
```

## 材料清单模板

`materials-checklist.md` 按高频材料整理：

```text
- 成绩单
- 成绩排名证明
- 专家推荐信
- 个人陈述/申请表
- 英语成绩证明
- 科研/竞赛/论文证明
- 身份证/学生证
- 其他院系指定材料
```

每个材料后标注哪些学校明确要求。

## 风险提示

必须写：

- 以官网最新通知为准；
- 截止时间可能含系统关闭时间，不要卡点提交；
- 第三方汇总可能滞后；
- 材料模板不能替代学校官方要求；
- 若通知涉及推免预选拔，要提醒读者认真阅读后续资格确认规则。

## 是否适合自动化

适合做每周自动化监测。

如果用户要求“每周提醒/持续监控/最近一周自动抓取”，可以创建自动化任务：

```text
每周固定搜索官方通知 -> 输出新增 camps.csv -> 生成 publish.md 摘要
```

但不要自动发布到平台。
