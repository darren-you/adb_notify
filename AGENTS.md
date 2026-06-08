# AGENTS

## Instruction Priority

- 规则冲突时，优先级依次为：用户当前明确要求 > 更近作用域的 `AGENTS.md` / `overrides` / 目录级规则 > 当前仓库真实代码、真实目录结构与真实 `deploy_config.sh` > 工作区 `harness/docs/workspace/standards/` 正文 > `README.md` 与 `harness/docs/workspace/harness/` 专题文档 > 历史归档与参考材料。
- 任何上层文档与真实代码、真实配置冲突时，先以真实现状为准，再决定是否需要回写文档或治理说明。

## General Rules

- 使用中文回复。
- 使用中文撰写文档。
- 生成 commit 时使用中文。
- 开始处理某个仓库前，优先阅读该仓库根目录 `README.md`；如果存在对应子工程 `README.md`，继续读取子工程说明后再动手。
- 当根 `README.md`、子工程 `README.md`、`deploy_config.sh`、实际目录结构之间出现不一致时，以当前仓库实际文件和配置为准，不要死记旧规则。
- 仅在故障排查、bug 修复、线上问题定位或明确需要复盘历史问题时，优先检索工作区根目录 `harness/docs/issues/` 中是否已有类似记录及解决方案。
- 对于明确的代码修改、文档修改、重构、实现新功能、纯说明类问题，不要求默认先检查上述问题归档目录。
- 在 `darren_space` 工作区内，新仓和历史仓的默认分支一律只允许 `master`；不允许新增 `main` 作为默认分支，也不允许继续保留 `main` 兼容逻辑。
- 如果发现某个仓库仍存在 `main` 默认分支或 `origin/main` 遗留引用，治理动作固定为：补齐 `master`、切换默认分支到 `master`、删除本地与远端旧 `main`，再继续后续治理。
- 在 `darren_space` 工作区内，如用户要求“全部提交并推送”“批量 pull/push 整个工作区”这类针对全工作区的 Git 操作，优先直接使用工作区根目录 `darren_space_git.sh`，不要逐仓库手动执行；除非用户明确要求只处理单个仓库，或该脚本不适用。
- 在 `darren_space` 工作区内，如任务明确属于子工程 `fast_deploy` submodule 同步，优先走 `workspace-fast-deploy-submodule-sync` Skill，不要长期直接在子工程内嵌的 `fast_deploy` 目录脱离源工程单独维护。
- 在 `darren_space` 工作区内，凡是面向人工在本地 terminal 直接执行的脚本 / CLI，默认终端输出都应遵循 `harness/docs/workspace/standards/tooling/terminal_output_golden_path.md`：优先块状摘要，颜色只做增强，机器可读模式保持纯文本。

## Engineering Standards

- 当前任务明确属于某个技术域时，除根 `README.md` 与子工程 `README.md` 外，还必须优先读取 `harness/docs/workspace/standards/README.md` 与对应 standards 正文。
- 如果当前任务明确属于某个技术域，但仓库内没有标准目录名，也应优先参考最接近的工作区 standards 文档，而不是只沿用历史实现。
- 标准冲突时，优先以工作区 `harness/docs/workspace/standards/` 正文和当前仓库真实结构为准。

## Documentation Layout

- 轻量仓库文档入口与归档边界统一以根 `README.md`、`harness/docs/README.md` 和工作区统一归档约定为准。

## Documentation Naming

- 对新增的项目文档文件（如 `.md`、`.markdown`、`.txt`），优先使用英文小写单词加下划线命名。
- `README.md` 作为特殊文档保留默认命名，不纳入普通文档命名规则。
- 历史文档、外部导入资料、第三方文档、截图说明、工具资料可以保留原始命名；不要为了满足命名规则批量重命名现有文件。
- 如果确实需要重命名已有文档，必须同时检查并更新仓库内的引用链接。
- 文档命名示例：`project_analysis_report.md`、`font_subset_extraction_guide.md`。

## Commit Message Record

- 当前工作区内每个子工程根目录统一维护 `commit_message.txt`，用于记录该子工程当前这次修改对应的提交信息。
- 每次在某个子工程完成修改后，都要覆盖写入该子工程根目录的 `commit_message.txt`，不要在文件中累积历史提交信息。
- `commit_message.txt` 的内容必须可直接用于提交：使用中文；第一行写 commit 标题；如有补充说明，第二行留空后继续写正文。
- 当用户要求提交某个子工程时，优先直接使用该子工程根目录 `commit_message.txt` 中已记录的内容作为 commit 信息；除非用户明确指定新的提交文案，否则不要临时改写成其他内容。
- 如果一次任务同时修改多个子工程，需要分别覆盖各自的 `commit_message.txt`。

## ADB Notify Scope

- 本仓库维护 USB 系统通知开关 Magisk 模块。
- 模块只处理“已连接到 USB 调试”通知和“正在通过 USB 为此设备充电”通知，不处理第三方前台服务通知。
- 生成的安装 zip 属于构建产物，默认不提交；正式可安装包通过 GitHub Release 发布。
- Magisk 模块相关行为优先参考 `harness/docs/workspace/standards/magisk_module/magisk_module_golden_path.md`，以及当前仓库 README 中的实际边界。
