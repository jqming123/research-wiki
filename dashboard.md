# Research Dashboard

> 日常入口。未安装 Dataview 时直接使用 [[index]]；以下查询均为可选增强。

## 快速入口

- [[index|完整内容目录]]
- [[log|最近操作记录]]
- [[inbox/README|Inbox 使用说明]]
- [[templates/paper|论文卡片模板]]
- [[templates/claim|科研主张模板]]
- [[templates/research-question|研究问题模板]]
- [[templates/synthesis|跨文献综合模板]]

## 待读与待深读论文

```dataview
TABLE citation_key AS "Citation", year AS "年份", status AS "状态", priority AS "优先级", summary AS "摘要"
FROM "wiki/papers"
WHERE status != "verified"
SORT priority DESC, year DESC
```

## 进行中的研究问题

```dataview
TABLE status AS "状态", priority AS "优先级", source_count AS "来源数", summary AS "摘要"
FROM "wiki/questions"
WHERE status != "answered" AND status != "archived"
SORT priority DESC, updated DESC
```

## 争议或未决主张

```dataview
TABLE claim_status AS "证据状态", confidence AS "信心", source_count AS "来源数", summary AS "摘要"
FROM "wiki/claims"
WHERE claim_status = "mixed" OR claim_status = "contradicted" OR claim_status = "unresolved"
SORT updated DESC
```

## 最近更新的综合

```dataview
TABLE scope AS "范围", source_count AS "来源数", updated AS "更新", summary AS "摘要"
FROM "wiki/synthesis"
SORT updated DESC
LIMIT 10
```
