# skills-for-me

[English](README_EN.md)

个人 Claude Code Skills 维护仓库。

## 简介

本仓库集中维护个人开发的 [Claude Code](https://docs.anthropic.com/en/docs/claude-code) Skills。

Claude Code Skill 是一种模块化的扩展包，通过提供专业知识、工作流程和工具集成来增强 Claude 的能力。每个 Skill 可以在 Claude Code 中通过命令触发使用。

## 技能目录

| 技能 | 命令 | 说明 |
|------|------|------|
| [task-splitter](task-splitter/) | `/task-splitter` | 将大型编码任务拆分为可跨会话执行的有序子任务 |
| [find-task](find-task/) | `/find-task` | 查找下一个未完成的子任务，制定实施计划并协助开发 |

## 仓库结构

```
skills-for-me/
├── archive/                        # 发布产物（.skill 打包文件）
│   ├── find-task.skill
│   └── task-splitter.skill
├── find-task/                      # find-task 技能源码
│   ├── SKILL.md
│   └── README.md
└── task-splitter/                  # task-splitter 技能源码
    ├── SKILL.md
    ├── README.md
    └── references/
        ├── task_overview_template.md
        └── subtask_template.md
```

## 安装方法

1. 从 `archive/` 目录获取对应的 `.skill` 文件
2. 解压文件：
   ```bash
   unzip task-splitter.skill
   ```
3. 将解压出的目录移动到 Claude Code 的 skills 目录：
   ```bash
   mv task-splitter ~/.claude/skills/
   ```
4. 重启 Claude Code 即可生效

## 使用方法

### task-splitter

与 Claude 讨论需求并确认方案后，输入 `/task-splitter` 即可将任务拆分为多个子任务文件，输出到项目的 `planning/` 目录。

详细说明请参阅 [task-splitter/README.md](task-splitter/README.md)。

### find-task

在新的会话中输入 `/find-task`，Claude 会自动查找下一个未完成的子任务，基于现有代码制定实施计划并协助开发。

详细说明请参阅 [find-task/README.md](find-task/README.md)。

## 添加新 Skill

1. 在仓库根目录下创建新的 skill 目录，包含 `SKILL.md` 文件
2. 按需添加 `references/`、`scripts/`、`assets/` 等资源目录
3. 编写 `README.md` 说明文档
4. 打包后将 `.skill` 文件存放到 `archive/` 目录
