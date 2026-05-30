# Skill Outputs

这个目录统一存放导师搜索、自媒体选题、夏令营监控三个 skill 的正式输出。

## 目录分区

```text
skill-outputs/
├── 01-direction-mentor-crawler/
├── 02-media-advisor-school-recommendation/
└── 03-physics-summer-camp-monitor-pack/
```

## 命名规则

导师/方向抓取：

```text
YYYY-MM-DD-school-college-direction-mentors/
YYYY-MM-DD-school-college-direction-map/
```

自媒体院校方向包：

```text
YYYY-MM-DD-school-college-direction-media-pack/
```

夏令营/推免信息监控：

```text
YYYY-MM-DD-date-range-topic-camp-monitor/
```

## 当前已有输出

```text
01-direction-mentor-crawler/
├── 2026-05-30-fudan-physics-official-research-directions-map/
└── 2026-05-30-pku-electronics-design-automation-computing-systems-mentors/

02-media-advisor-school-recommendation/
├── 2026-05-30-fudan-physics-optical-science-media-pack/
└── 2026-05-30-fudan-physics-quantum-media-pack/

03-physics-summer-camp-monitor-pack/
└── 2026-05-30-2026-05-24-to-2026-05-30-physics-camps-monitor-test/
```

## 使用约定

- 正式产物只放进 `skill-outputs/`。
- 每次运行单独建一个小文件夹，不覆盖旧结果。
- 文件夹名必须能看出日期、对象和内容类型。
- 临时草稿可以放旧目录，但最终交付前要迁移到这里。
