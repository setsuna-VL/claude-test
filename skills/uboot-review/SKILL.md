---
name: uboot-review
description: Ingenic ISVP U-Boot代码审查技能。审查指定commit的代码变更，基于模板生成评审文档。
---

# Skill: uboot-review

## Purpose
这个技能帮助用户review U-Boot代码。

## Trigger Conditions
当用户提到以下内容时会触发此技能：
- "uboot-review 审查"
- "uboot-review --commit"

# U-Boot代码审查

## 核心原则

**绝对禁止**：
- 假设/假装/猜测任何信息
- 未经验证就下结论
- 跳过任何检查项
- 编造不存在的问题或忽略存在的问题

**必须做到**：
- 实事求是，有一说一
- 每个结论必须有代码依据（引用具体行号）
- 不确定的标注"需人工确认"

## 执行流程

### 1. 获取提交信息

```bash
git show <hash> --stat
git show <hash> -p
git log -1 --format="%s%n%b" <hash>
```

提取：芯片型号、修改简述、提交日期

### 2. 生成评审文档

```bash
cp /home_a/oywei/.claude/plugins/cache/ingenic-skill/ingenic-isvp-code-review/1.0.0/skills/uboot-review/references/芯片型号-修改简述-日期.md ./<芯片型号>-<U-Boot-版本>-<修改简述>-<YYYYMMDD>.md
```

文件名示例：`PRJ008_ZN-U-Boot-2013-新增efuse读取-20260203.md` 或者 `PRJ008_ZN-U-Boot-2022.10-新增efuse读取-20260203.md`

### 3. 审查与检查

**先读取模板：**
```bash
cat /home_a/oywei/.claude/plugins/cache/ingenic-skill/ingenic-isvp-code-review/1.0.0/skills/uboot-review/references/芯片型号-修改简述-日期.md
```

**然后：**
1. 按模板中各章节逐项填写评审文档，信息不足标注"需补充"
2. 按模板中"检查点"章节逐项审查，每项给出具体依据

**自查结果格式**：
- ✓ 通过：具体说明
- ✗ 不通过：具体问题
- N/A：不涉及
- ? 需人工确认：原因

**检查通知**
检查完需把检查点表格作为结果完整输出（不仅仅是写到文档中）

### 4. 评审总结

汇总发现的问题，给出评审意见：
- 可入库
- 需修改后入库（列出问题）
- 不建议入库（列出原因）

## 输出

完成后告知用户评审文档路径，并完整列出 检查点 表格和关键发现。
