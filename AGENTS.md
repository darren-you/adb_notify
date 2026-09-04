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
- 在 `darren_space` 工作区内，GitHub 仓库名固定使用小写下划线风格：只允许小写字母、数字和 `_`，例如 `auth_service`、`template_project`；`darren-you/darren-you` 是 GitHub Profile README 平台规则要求的唯一例外，不能改成下划线命名。
- 在 `darren_space` 工作区内，新仓和历史仓的默认分支一律只允许 `master`；不允许新增 `main` 作为默认分支，也不允许继续保留 `main` 兼容逻辑。
- 如果发现某个仓库仍存在 `main` 默认分支或 `origin/main` 遗留引用，治理动作固定为：补齐 `master`、切换默认分支到 `master`、删除本地与远端旧 `main`，再继续后续治理。
- 在 `darren_space` 工作区内，如用户要求“全部提交并推送”“批量 pull/push 整个工作区”这类针对全工作区的 Git 操作，优先直接使用工作区根目录 `darren_space_git.sh`，不要逐仓库手动执行；除非用户明确要求只处理单个仓库，或该脚本不适用。
- 在 `darren_space` 工作区内，如任务明确属于子工程 `fast_deploy_core` submodule 同步，优先走 `workspace-fast-deploy-submodule-sync` Skill，不要长期直接在子工程内嵌的 `fast_deploy_core` 目录脱离源工程单独维护。
- 在 `darren_space` 工作区内，人工可读的展示名称统一使用 `Fast Deploy`（标题式）或 `fast deploy`（句中普通文本）；`fast_deploy_panel`、域名、路径、服务名、API 和代码符号等技术标识按真实值保留。外部原样导入的第三方源码中，与工作区产品无关的上游专名按原始命名保留。
- 在 `darren_space` 工作区内，凡是面向人工在本地 terminal 直接执行的脚本 / CLI，默认终端输出都应遵循 `harness/docs/workspace/standards/tooling/terminal_output_golden_path.md`：优先块状摘要，颜色只做增强，机器可读模式保持纯文本。

## Engineering Standards

- 当前任务明确属于某个技术域时，除根 `README.md` 与子工程 `README.md` 外，还必须优先读取 `harness/docs/workspace/standards/README.md` 与对应 standards 正文。
- 如果当前任务明确属于某个技术域，但仓库内没有标准目录名，也应优先参考最接近的工作区 standards 文档，而不是只沿用历史实现。
- 标准冲突时，优先以工作区 `harness/docs/workspace/standards/` 正文和当前仓库真实结构为准。
- 所有纳管产品的关系型数据库、MongoDB / GridFS、Redis、SQLite、本地持久化、Schema、迁移、查询与事务、备份恢复，以及数据库字段到领域模型、DTO、OpenAPI 和客户端的映射，统一遵循 `harness/docs/workspace/standards/database/database_golden_path.md`。发现漂移时必须先修改真实 Schema / 迁移 / 源码及全部真实消费者，再同步文档和生成视图；禁止只改 AGENTS、README 或规范文本后宣称产品已经合规。

## Documentation Layout

- 轻量仓库文档入口与归档边界统一以根 `README.md`、`harness/docs/README.md` 和工作区统一归档约定为准。

## Documentation Naming

- 对新增的项目文档文件（如 `.md`、`.markdown`、`.txt`），优先使用英文小写单词加下划线命名。
- `README.md` 作为特殊文档保留默认命名，不纳入普通文档命名规则。
- 历史文档、外部导入资料、第三方文档、截图说明、工具资料可以保留原始命名；不要为了满足命名规则批量重命名现有文件。
- 如果确实需要重命名已有文档，必须同时检查并更新仓库内的引用链接。
- 文档命名示例：`project_analysis_report.md`、`font_subset_extraction_guide.md`。

## Commit Message Record

- 当前工作区内每个 Git 根目录统一且仅维护根部一个 `commit_message.txt`，它只记录尚未进入本地提交的变更意图；普通子目录和 path-scoped 工程继承所属 Git 根记录，禁止另建同名文件。尚未 push 的本地提交由 Git ahead 状态表达，不再把已进入 commit body 的记录留在文件中。
- 开始修改某仓库前，必须先检查工作树、暂存区与 `commit_message.txt`：仍有未提交变更或已有记录时，保留已有条目并追加本次摘要；两者都为空时，从空文件写入本次条目。不得因仓库存在 ahead commit 而恢复或复制已经进入 Git 历史的记录。
- `commit_message.txt` 只允许使用 Markdown 无序列表：每个独立变更占一行，格式固定为 `- <中文变更摘要>`；不写标题、空行或列表外正文，不重复已有条目。
- 任何自动化只要产生目标仓的源码、文档、配置或 gitlink 变更，就必须在同一次操作中为该 Git 根追加合法且不重复的记录；自动化应在同一 Git 根记录锁内按“实际文件写入 → 记录追加”完成，无法跨文件写入持锁时也必须先落真实变更、最后再追加记录，禁止先记录、释放锁后再写文件。记录更新与 `darren_space_git.sh` 的本地 prepare 必须使用同一把锁。
- `darren_space_git.sh push` 在本地 prepare 中对合法非空记录取快照，将第一条写入 commit 标题、完整列表写入 commit body；缺失、为空或临时不合法时使用中性记录 `- 保存当前工作区快照（任务可继续进行）`，不得把摘要未完成当作拒绝保存代码的依据。planned commit 跟踪空记录文件，缺失文件在本地创建为空；不合法原文保留在工作树，合法记录只消费本轮快照，后来新增或改写的内容保留到下一轮。记录文件为符号链接、目录等不安全写入对象时仍拒绝。非 Git 根同名文件违反编写规范，但不阻断 push。网络 push 失败时不得恢复或复制已进入 commit body 的记录。
- 当用户要求提交某个子工程时，优先使用该仓库合法非空 `commit_message.txt` 的第一条生成 commit 标题，并将完整无序列表写入 commit body；否则按上述快照摘要保存，除非用户明确指定新文案，不推断或改写任务完成结论。
- 如果一次任务同时修改多个子工程，必须分别更新各自的 `commit_message.txt`；批量 push 通知从各 planned SHA 的 Git commit body 读取记录，并按“项目名: 7 位 commit SHA”分组展示。

## Client API Response Contract

- 普通 REST JSON 的客户端 DTO 与真实网络解码入口必须共同遵守 `code / timestamp / msg / data` 四字段合同；不能把 TypeScript 类型断言、Swift 合成解码或模板文件一致当作运行时验证。`timestamp` 与 `msg` 必需，`data:null` 不能与缺少 `data` 混同；拒绝额外顶层字段、旧 `message`、旧成功码 `0` 和裸业务 JSON 兼容路径。
- Auth 错误按 OpenAPI 的 `data.error_code / trace_id` 解析，禁止退回旧 `data.error.code/message`。HTTP 失败和业务失败均不能被客户端当作成功返回；health 按同一 envelope 读取 `data.service`。
- 新增或修改 DTO、JSON 网络读取、错误映射时，必须同时运行 `python3 harness/scripts/check_client_response_contract.py --repo <逻辑仓库名>` 与该工程真实请求/解码回归；回归至少覆盖成功、失败、null、缺字段、额外字段和旧格式。Web 的 DTO 回归必须进入实际 `npm run build` 链路，不能只留下不会执行的测试文件；Swift 测试必须进入实际使用的 SwiftPM / Xcode target。
- 客户端合同检查由工程标准、总治理和对应构建发布链路执行；Git push 与 dry-run 只负责保存和传输代码快照，不执行该质量检查，允许 task 在未完成时保存。发现新解析形态时扩展检查器及失败回归，不能添加产品白名单或仅靠 AGENTS 口头保证；push 成功不能替代构建、测试和发布验证。完整边界见 `harness/docs/workspace/standards/client_response_contract.md`。

## ADB Notify Scope

- 本仓库维护 USB 系统通知开关 Magisk 模块。
- 模块只处理“已连接到 USB 调试”通知和“正在通过 USB 为此设备充电”通知，不处理第三方前台服务通知。
- 生成的安装 zip 属于构建产物，默认不提交；正式可安装包通过 GitHub Release 发布。
- Magisk 模块相关行为优先参考 `harness/docs/workspace/standards/magisk_module/magisk_module_golden_path.md`，以及当前仓库 README 中的实际边界。
