# AI 自媒体项目

做企业 AI 赋能方向的 AI 产品经理，业余做 AI 短视频 + 公众号。目标：扩大行业影响力、为下一次求职做「视频简历」、践行「让每个人做自己喜欢的事并养活自己」。节奏：每周 1-2 条，先试水。

## 内容生产流水线（5 个 agent）

所有 agent 工作前都会先读 `内容大脑.md`（人设/三目的/内容支柱/钩子/语气/合规），保证口径统一。

| Agent | 干什么 | 怎么触发 | 输出 |
|---|---|---|---|
| `ai-news` | 收集当日 AI 资讯，PM 视角过滤解读 | "今天有什么 AI 资讯" | `资讯简报/日期.md` |
| `topic-picker` | 产出带钩子的选题，三目的打分 | "帮我选题" | 更新 `选题库.md` |
| `script-writer` | 选题→60-90 秒口播稿 | "把 XX 写成口播稿" | `口播稿/序号-标题.md` |
| `article-writer` | 选题/口播稿→公众号文章 | "写成公众号" | `公众号/标题.md` |
| `comment-collector` | 浏览器抓评论并分析 | "收集我最新视频的评论" | `评论反馈/日期.md` |

**典型一周**：ai-news 找灵感 → topic-picker 定选题 → script-writer 出稿拍摄 →（可选）article-writer 扩成公众号 → 发布后 comment-collector 分析反馈 → 洞察回流下一轮选题。

## 关键文件

- `内容大脑.md` —— agent 共享上下文（改定位就改这里，所有 agent 自动跟着变）
- `对标账号.md` —— 权威资讯源 + 对标博主/公众号清单（ai-news 抓料、topic-picker 判热度用）
- `选题库.md` —— 滚动选题 backlog
- `起号方案.md` / `企业AI落地-内容素材库.md` / `两周试水计划.md` —— 策略与素材

## Git / 版本管理

本项目用 git 管理，远程为 GitHub **私有**仓库 `gongbenxi/AI-videoCreat`（分支 `main`）。

**工作约定：只要项目文件有改动或新增（新简报、口播稿、公众号、选题更新、策略调整等），就提交并推送。** 用 Claude 做完一组改动后，主动执行：
```bash
git add -A && git commit -m "<简述改动>" && git push origin main
```
- 推送需本机代理：`export HTTPS_PROXY=http://127.0.0.1:7897 HTTP_PROXY=http://127.0.0.1:7897`（终端已配置自动跟随系统代理；Clash 换端口会自动更新）。若代理不通，git 凭据已配好，可直连推送。
- `.claude/settings.local.json` 和 `.DS_Store` 已在 `.gitignore` 中排除，属本机个人配置，不入库。

## 备注

- 每天早上 7 点有定时任务 `daily-ai-news-brief` 自动跑 ai-news、生成当天简报并推送（本机 Claude 应用开着时运行，没开则下次启动补跑）。
- `comment-collector` 依赖 Claude in Chrome 扩展已连接、平台已登录；抓取失败会降级为「手动粘贴评论」。
