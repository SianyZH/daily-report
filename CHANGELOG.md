# 迭代日志 CHANGELOG

> 本文件记录「智能日报系统」前端每次部署的迭代内容，按日期倒序排列。
> 线上地址：https://sianyzh.github.io/daily-report/
> 分支策略：`dev` = 开发/预发分支；合并到 `main` 即发布（GitHub Pages 源 = main 分支根目录）。

---





## 2026-08-07

- style: 日报表格优化-转任务改小图标按钮(悬停提示) 描述列加宽一倍 全控件统一36px高 状态列加宽防裁字

## 2026-08-06

- feat: Sprint2 F5任务进度%卡片迷你条+详情滑块(已完成自动100%) F6跟进页筛选器(优先级/到期/创建人)
- feat(Sprint 1): F1 任务优先级(🔴高🟡中⚪低)+卡片色块+看板排序+详情改; F2 在手任务总览条(可点击过滤); F3 日报↔tasks表双向同步; F4 日报表单🔗/📝行类型标识; F4b 三个任务创建入口(转任务/新建任务弹窗/子任务)
- fix: 任务写操作(保存/新增/删除子任务、保存主任务)前置 JWT 守卫，过期引导重登不再丢数据; toast 支持自定义时长
- feat: 任务跟进加周期锚点导航——周/月视图支持 ◀ ▶ 切换上/下周期、📅 选择具体周/月、⏎ 回到今天
- fix: t-note textarea 补 rows=1 与 t-desc 同高；状态列加宽 112px+select 内边距收窄文字不再截断；date input 恢复原生外观保证日期面板可弹
- fix: td 改回 table-cell + cell-wrap 内部 flex 对齐，修复上一轮 appearance:none + td flex 导致的表格布局崩溃
- fix: 控件appearance:none+padding:10/6+min-height 34+自定义下拉箭头，三控件实际渲染高度完全一致
- fix: 表格所有td统一flex-start+三控件padding/min-height完全统一，文字基线严格对齐
- fix: textarea 默认压成一行(min-height 34,rows=1)+JS 自动增高;状态/到期 padding-top 降为 10 与描述齐平
- fix: 表格内控件 padding-top 14px+min-height 56px 让序号/状态/到期明显视觉居中
- fix: 表格内控件垂直居中——状态/到期列改flex容器不再高低不齐
- fix: 表格5列顶部不对齐——统一table.tasks td顶padding为6px(原为0/0/14px/6px/6px多档错位)、.tnum取消14px hack改flex-start、select.t-status显式高度与input.t-due对齐，三列控件顶部精确同水平线
- refactor: 到期日拆为独立第4列——表格升级为5列(#/任务描述/状态/到期/结果·产出·进展)，移除全部绝对定位代码(.t-due-row/.col-res position:absolute)，到期作为普通td单元格彻底根治错行
- fix: 第4列日期错行——改为 div.col-res(block) 作 position:relative 包含块承载绝对定位的日期input(td上position:relative不可靠)，修正 .col-res 宽度选择器(38%/42%→100%)与 textarea 让位选择器(td.col-res→.col-res + !important 防移动端覆盖)
- fix: 填日报表格第4列日期对齐——用绝对定位把📅+日期input 嵌在备注textarea右下角，整列只占一个textarea的高度、跟其他列高度对齐，彻底告别错行
- refactor: 填日报表格第4列样式修复——移除 task-meta flex 包装(日期input独占整行)，改为 textarea 占满顶部、t-due-row 行内紧凑显示(📅到+日期input)，不再有错位空白

## 2026-08-05

- refactor: 子任务管理统一收口到任务跟进页——填日报表单移除子任务输入(只保留描述/状态/备注/到期)，详情弹窗加子任务列表+添加+删除+状态/到期/备注编辑+主任务状态/到期/备注编辑
- fix: 任务跟进页面空白——switchPage 的 page 数组漏了 follow 导致 page-follow 永远停留在 hidden
- fix: 历史日报回填状态推断——fillFormFromRecord 不再用 normalizeStatus 强制兜底"进行中"，t.status 缺省时走 inferStatus 从 result/note/desc 推断；note 回填补强空字符串兜底
- fix: 修复日报表格列错位——thead补齐第4列(状态/结果-备注)与tbody的4个td对齐，根治table-layout:fixed下多td被错位填充
- feat: 任务跟进系统——新建 tasks 表+迁移51条历史任务+日/周/月视图看板+子任务+角色视图(我的/下属/团队)+日报提交同步写tasks

## 2026-07-28

- fix: 修复日报日期错位——init 清理日历导入残留 pending 日期 + 页面重新可见时自动校正非手动选择的过去日期，根治长时间开页面导致日报误存旧日

## 2026-07-27

- fix: 日历授权回调同步刷新 Supabase 登录态，根治登录 JWT 过期导致日历导入反复报 401；后端 v22 增强 authGuard 失败审计
- fix: 日历授权回调同步刷新 Supabase 登录态，根治登录 JWT 过期导致日历导入反复报 401；后端 v22 增强 authGuard 失败审计
- fix: 钉钉日历导入修复——授权回跳后还原所选日期(根治跳回今天)；失败显示钉钉真实报错且杜绝重授权死循环；后端写日历失败审计日志(v21)
- **fix(后端 v20)**: 根治「账号邮箱对应错误身份」——邮箱改由 SHA-256(unionId) 规范派生（抗碰撞、不再小写化）；更新既有账号时强制同时重写 email+user_metadata，保证「邮箱≡union_id」铁律，杜绝邮箱属A身份属B的漂移。部署 Edge Function v20。
- fix: 钉钉登录失败时展示完整诊断字段(foundBy/userId/email/putError/hint)；清理漂移账号
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
