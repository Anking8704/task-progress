---
name: task-progress
description: Keep a live task checklist (plan) visible to the user while working. Use at the start of EVERY task that edits files, runs more than one command, or has several steps (implement-and-test, investigate-then-fix, install/configure, anything the user listed). Skip only for a single-command answer or pure conversation.
---

# Task Progress

Keep the task checklist current and visible to the user. Display depends on the host: in some Codex desktop versions the list is shown on hover over the progress indicator while the turn is active.

## Tool

Use the built-in `update_plan` tool. Each call sends the WHOLE list:

```json
{
  "explanation": "optional one-line reason for a change",
  "plan": [
    {"step": "查看现有配置", "status": "completed"},
    {"step": "实现扫码配对", "status": "in_progress"},
    {"step": "测试并安装", "status": "pending"}
  ]
}
```

`status` is one of `pending`, `in_progress`, `completed`.

If `update_plan` is not available, or the user needs a checklist visible in chat, print the same list as Markdown, using `- [x]` for completed, `- [ ] ⏳` for in progress and `- [ ]` for pending. Reprint it whenever it changes. When the tool is available, continue updating it even if you also display Markdown.

## Rules

1. **Plan first.** Before or together with your first real action (even a read-only look around), call
   `update_plan` with the whole plan in order. If you must explore first, make step one
   "查看 X 的现状" and refine the list once you know more.
2. **Short steps.** 3–8 steps, each a short imperative phrase (about 4–12 Chinese characters or ≤7 English
   words), in the user's language. No numbering — the list is ordered already.
3. **Exactly one `in_progress`** while working. Never several at once, never zero mid-task.
4. **Advance as you go.** When a step finishes, mark it `completed` and the next one `in_progress` in the
   same call, right when you start that next step. Don't batch several completions at the end.
5. **Plan changed? Resend the whole list.** If you discover new work, drop a step, or the user redirects
   you mid-task, call `update_plan` with the new full list (use `explanation` to say why), so the shown
   list never describes an abandoned plan.
6. **Don't duplicate.** Don't also write the plan as a numbered list in your message; a Markdown checklist may be used when needed for visibility.
7. **Finish cleanly.** When everything is done, mark every step `completed`, then end with a 2–3 sentence
   recap: what is now true, and anything not done or not verified (e.g. "未提交", "未在真机上测试").
   Report failures honestly — a step whose check failed is not `completed`; say what failed.

## Example

User: "把结果图设为输入图，并让查看器支持左右滑动切换"

1. First call (with your first file read):
   查看相关代码 `in_progress` · 结果图设为输入图 `pending` · 查看器左右滑动切换 `pending` · 测试并汇报 `pending`
2. After reading, starting the edit: 查看相关代码 `completed` · 结果图设为输入图 `in_progress` · …
3. Found the iPad layout also needs work → resend the whole list with a new step "适配 iPad 布局".
4. End: all `completed`, then the recap.

