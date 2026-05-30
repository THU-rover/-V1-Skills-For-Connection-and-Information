---
name: media-advisor-school-recommendation
description: Use when creating Chinese self-media publishing packages for physics baoyan audiences that combine school/direction introductions, advisor/lab mining, official-source summaries, XMind direction-teacher maps, admissions/exam-form notes, and recommendation-style content for manual publishing.
---

# 自媒体创作 | 导师挖掘院校推荐

## 统一输出目录

所有本 skill 生成的内容，统一放在用户工作区：

```text
skill-outputs/02-media-advisor-school-recommendation/
```

每一次输出必须单独建一个小文件夹，文件夹名要能直接看出“日期 + 学校 + 学院/方向 + 内容类型”：

```text
YYYY-MM-DD-school-college-direction-media-pack/
```

示例：

```text
skill-outputs/02-media-advisor-school-recommendation/2026-05-30-fudan-physics-optical-science-media-pack/
skill-outputs/02-media-advisor-school-recommendation/2026-05-30-pku-electronics-optical-communication-media-pack/
```

不要把正式产物散放在 `publish-packs/` 根目录；`publish-packs/` 只作为旧产物或临时草稿目录。

这个 skill 用来做物理保研自媒体内容，不是给某一个学生做私人择导。它的核心任务是：

```text
官方信息收集 -> 院校/方向拆解 -> 导师/课题组线索整理 -> 自媒体文案与卡片包
```

## 什么时候使用

适合：

- 做“27物理保研方向院校方向介绍｜某方向”栏目；
- 整理某学校某学院的研究方向；
- 把某方向下的导师/课题组按子方向归类；
- 给小红书/公众号/视频号准备方向介绍、院校推荐、导师挖掘内容；
- 需要同时输出 XMind Markdown、卡片文案、发布文案、来源表和检查表。

不适合：

- 承诺上岸概率；
- 给单个学生做最终择导决策；
- 无来源地搬运、复制官网全文；
- 把编辑归纳说成学校官方结论。

## 是否要和导师挖掘 skill 联用

不一定。

如果只是写一篇方向科普，且官网方向页已经列出导师和研究内容，可以只用本 skill。

如果要“尽量完整地抓某方向下的导师/课题组”，建议联用方向级导师爬取 skill：

```text
direction-mentor-crawler：负责抓列表页、导师详情页、覆盖检查
media-advisor-school-recommendation：负责整理成自媒体内容和方向地图
```

推荐分工：

1. **信息采集**：用爬虫/方向级导师 skill 找官方方向页、师资页、导师页。
2. **信息核验**：生成 `official-links.csv`、`direction-teachers.csv`、`admission-notices.csv`。
3. **自媒体转化**：用本 skill 生成标题、正文、卡片、XMind Markdown、检查表。

## 输出文件夹

创建：

```text
publish-packs/YYYY-MM-DD-topic-slug/
├─ source/
│  ├─ official-links.csv
│  ├─ source-notes.md
│  ├─ admission-notices.csv
│  └─ direction-teachers.csv
├─ brief.md
├─ mindmap-xmind.md
├─ cards/
│  ├─ 01-cover.md
│  ├─ 02-what-is-this-direction.md
│  ├─ 03-official-map.md
│  ├─ 04-sub-directions.md
│  ├─ 05-teacher-map.md
│  ├─ 06-who-fits.md
│  ├─ 07-exam-format.md
│  └─ 08-action-list.md
├─ publish.md
└─ checks.md
```

## 标题规则

默认标题格式：

```text
27物理保研方向院校方向介绍｜<方向名>
```

例子：

```text
27物理保研方向院校方向介绍｜光物理光科学方向
27物理保研方向院校方向介绍｜理论与计算物理方向
27物理保研方向院校方向介绍｜凝聚态物理方向
```

`publish.md` 中给 3-5 个标题备选，第一条默认使用这个格式。

## 正文必须包含

正文不能太短，至少包含三部分：

1. **这个方向是什么**
   - 用通俗话解释。
   - 说明研究对象、常见问题、和普通课程名的区别。

2. **这个学校的这个方向包含哪些细方向**
   - 从官网方向页、师资页、课题组页提炼。
   - 按子方向桶组织。
   - 说明这是编辑归纳，不是官方分组，除非官网明确这么分。

3. **往年考核方式**
   - 搜集官方夏令营、推免、复试通知。
   - 写清形式：现场/线上、面试/笔试/讲座、考核内容、时长、权重。
   - 必须提示：往年仅供参考，以当年最新通知为准。

## XMind Markdown 规则

`mindmap-xmind.md` 只包含方向和导师：

```markdown
# 学校学院：方向名

## 子方向A

### 老师1

### 老师2

## 子方向B

### 老师3
```

不要在 XMind Markdown 里放：

- 夏令营信息；
- 考核方式；
- 来源链接；
- 文案话术；
- 行动建议。

这些内容放到 `publish.md`、`cards/07-exam-format.md` 和 `source/admission-notices.csv`。

## 来源表要求

`official-links.csv` 至少包含：

```text
类型,名称,URL,本次状态,备注
```

`admission-notices.csv` 建议包含：

```text
年份,通知类型,官方链接,活动/复试形式,考核内容,成绩/权重,备注
```

`direction-teachers.csv` 建议包含：

```text
子方向桶,教师,官网研究内容摘要
```

## 卡片结构

默认 8 张：

1. 封面：栏目标题 + 核心判断。
2. 方向是什么：通俗解释。
3. 官方入口：官网路径和来源。
4. 细方向拆解：方向桶。
5. 导师地图：子方向下有哪些老师。
6. 谁适合：适合什么背景/兴趣的学生。
7. 考核方式：往年夏令营/复试形式。
8. 下一步：怎么继续查。

## 写作规则

- 语气：像靠谱的学长/编辑，不像营销号。
- 不要写“稳了”“上岸概率高”“闭眼冲”。
- 不要把学校方向包装成绝对排名。
- 不要大段复制官网。
- 用“官网显示/官网方向页列出”表达事实。
- 用“可以粗略拆成/为了方便理解”表达编辑归纳。
- 所有具体事实必须能在来源表中找到出处。

## 检查清单

`checks.md` 至少检查：

- [ ] 官方来源已列入来源表
- [ ] 正文包含“方向是什么”
- [ ] 正文包含“该学校该方向的细方向”
- [ ] 正文包含“往年考核方式”
- [ ] XMind Markdown 只包含方向和导师
- [ ] 已区分官方事实和编辑归纳
- [ ] 没有承诺录取结果
- [ ] 已提示往年信息仅供参考
