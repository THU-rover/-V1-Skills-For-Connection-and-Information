# -V1-Skills-For-Connection-and-Information

懒得扒导师？懒得理方向？懒得追夏令营？把官网整理成能看懂、能发布、能复查的资料包。

中文 description：

> 给物理/电子保研人用的院校情报小铲子：扒导师、理方向、追夏令营，把官网迷宫整理成能看懂、能发布、能复查的资料包。

这个仓库收集了三个本地 Codex skill，用来辅助保研信息整理和自媒体内容生产。

## 包含内容

```text
skills/
├── direction-mentor-crawler/
├── media-advisor-school-recommendation/
└── physics-summer-camp-monitor-pack/

examples/
└── skill-outputs/
```

## 三个 Skill

`direction-mentor-crawler`

方向级导师抓取。适合从某个学院、系、方向或实验室的师资列表页出发，抓取导师详情页，并生成覆盖检查表。

`media-advisor-school-recommendation`

自媒体院校方向介绍包。适合把某个学校某个方向整理成正文、卡片文案、XMind Markdown、来源表和事实核查表。

`physics-summer-camp-monitor-pack`

物理保研夏令营信息抓取。适合按时间范围搜索近期夏令营、推免、预报名通知，重点整理截止时间、申请材料、考核方式和官方链接。

## 输出目录约定

正式输出统一放在：

```text
skill-outputs/
├── 01-direction-mentor-crawler/
├── 02-media-advisor-school-recommendation/
└── 03-physics-summer-camp-monitor-pack/
```

每次运行单独生成一个小文件夹，文件夹名要包含日期、学校/方向/时间范围和输出类型。

示例：

```text
2026-05-30-pku-electronics-design-automation-computing-systems-mentors/
2026-05-30-fudan-physics-optical-science-media-pack/
2026-05-30-2026-05-24-to-2026-05-30-physics-camps-monitor-test/
```

## 注意

- 只使用公开网页和官方通知做事实依据。
- 自媒体文案里的判断需要区分“官方事实”和“编辑归纳”。
- 夏令营和推免信息会变化，发布前必须回到官方链接复核。
- 示例输出仅用于展示文件结构和工作流，不代表长期有效信息。
