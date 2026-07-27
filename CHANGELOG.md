# 迭代日志 CHANGELOG

> 本文件记录「智能日报系统」前端每次部署的迭代内容，按日期倒序排列。
> 线上地址：https://sianyzh.github.io/daily-report/
> 分支策略：`dev` = 开发/预发分支；合并到 `main` 即发布（GitHub Pages 源 = main 分支根目录）。

---

## 2026-07-27

- fix: 日报详情弹窗结果/状态始终展示（彩色状态徽章+空态标注），头部显示结果已填X/Y；填表结果列加输入提示
- chore: 前端接入 dev 分支工作流，部署须走 dev→main 并自动同步 CHANGELOG
- **feat**: 日报列表新增「查看详情」弹窗，完整展示每条任务的「描述 + 结果/状态」，不再截断为"…"
- **fix**: 修复 GitHub Pages 子路径下钉钉 OAuth `redirect_uri` 缺失 `/daily-report/` 导致回调 404
- **fix**: 钉钉登录改用 GitHub Pages 完整地址后回调正常
- **refactor**: 前端迁移至 GitHub Pages 永久托管（弃用 CloudStudio 沙箱与 Vercel）
- **feat**: 引入 `dev` 分支 + 本 CHANGELOG，规范迭代内容记录

## 2026-07-23

- **fix**: 前端 `init()` 改为最先绑定事件，修复"点击提交无反应"
- **feat**: 新增「预览提示词」按钮，可见完整输入含【岗位职责】
- **feat**: 周报/月报模板增加 ≤500 字硬性限制（写入系统提示词规则 #8）
- **fix**: 月报模板 `data.monthlyPrompt` 笔误导致 `undefined`，已修复为 `data.monthly_prompt`

## 2026-07-22

- **refactor**: 身份模型重构，身份锚点改为不可篡改的钉钉 `union_id`（关闭"改名冒充"漏洞）
- **security**: 安全加固 P0/P1/P2 全修复（受保护端点 JWT 校验、audit_log 审计、隐私政策弹窗）
- **feat**: DeepSeek Key 改为「全局 + 主密码」模式，跨设备免重填
- **fix**: 同事登录 `Invalid login credentials` —— Edge Function v18 改用 `HMAC(unionId)` 确定性密码派生

---

*格式约定：每条以 `type: 说明` 记录，`type` ∈ {feat 新功能, fix 修复, refactor 重构, security 安全, docs 文档, chore 杂项}。*
