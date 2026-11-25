# Fitness Ledger · 运动计划与记录

给 Codex 使用的中文 Agent Skill。它让跑步、力量、攀岩、饮食和体测聊天共用一个 Notion 项目，并按主睡眠醒来的时间归档。例如，凌晨一点跑完步、吃了东西又去睡，训练和餐食继续归到醒着的那个作息日。午睡不会另开一天。

Skill 包含[训练计划与专项记录](skills/fitness-ledger/references/event-records.md)、[作息日与每日双汇总](skills/fitness-ledger/references/sleep-day.md)和[每周维护](skills/fitness-ledger/references/weekly-review.md)。建议、已确认的计划和实际训练分别保存，跨聊天补报可以追溯回原事件。

## 安装

从 [Releases](https://github.com/kuoyang1999/fitness-ledger-skill/releases) 下载 `fitness-ledger.zip`，解压后把 `fitness-ledger` 文件夹放进个人 Codex skills 目录（默认 `~/.codex/skills/`）。也可以把下面这句话发给有 GitHub 访问能力的 Codex，让它完成安装。

> 请从 GitHub 仓库 kuoyang1999/fitness-ledger-skill 安装 skills/fitness-ledger，只安装这个 Skill。

手动安装可在终端运行以下命令。目标目录已存在时，保留已有版本，再决定是否更新。

```sh
git clone https://github.com/kuoyang1999/fitness-ledger-skill.git
skills_dir="${CODEX_HOME:-$HOME/.codex}/skills"
mkdir -p "$skills_dir"
test ! -e "$skills_dir/fitness-ledger" && cp -R fitness-ledger-skill/skills/fitness-ledger "$skills_dir/"
```

在新聊天中输入 `$fitness-ledger` 并说明任务。首次使用时，在自己的聊天中提供 Notion 项目入口、默认时区和需要维护的专项。若希望读取睡眠，使用已连接并允许读取本人 Apple Health 的环境。也可以直接报告最终醒来时间。安装本 Skill 后，周检和双汇总都可手动调用。定时运行需单独设置。

## 三种用法

**给跑步、力量、饮食或身体测量的新聊天**

> 使用 $fitness-ledger 接手我的【专项名称】记录。项目入口是【我自己的 Notion 链接】，默认时区是【IANA 时区】。先读索引、当前已确认计划、最近一次原记录和待核项。以后用这个专项原库记实际事件，补报时更新原记录。先告诉我目前的计划以及下一次需要核对什么。

**给每日运动双汇总**

> 使用 $fitness-ledger 维护每日运动双汇总。先核对本人报告和 Apple Health 的主睡眠，用最终醒来划分作息日。如果缺设备记录，用近期同作息环境的数据评估能否推定并标出依据。午间写截至当前的快照，取得下次主醒来后再做最终日结。补同步改变边界时，重查受影响的原事件。

**给每周维护聊天**

> 使用 $fitness-ledger 检查上一完整周的作息标签和上次检查后的补录。核对训练、餐食、体测、计划进度及页面归属。修正证据充分的局部问题，回读后在既有维护日志写下检查范围和未决事项。只在有新发现、状态变化或需要我决定时通知我。

项目地址、设备导出、真实记录和个人目标放在自己的私有项目。这个仓库只发布工作方法，所有演示情境均为虚构。
