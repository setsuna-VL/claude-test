# Ingenic Skill Marketplace

Ingenic ISVP 开发技能集，用于 Claude Code。

## 安装

```bash
/install-plugin github:<用户名>/ingenic-skill
```

## 包含技能

### ingenic-isvp-code-review

U-Boot 代码审查技能。

**使用方法：**
```
/uboot-review --commit <hash>
```

**功能：**
- 获取指定 commit 的变更信息
- 按模板生成评审文档
- 逐项检查代码规范
- 输出检查点表格和评审意见
