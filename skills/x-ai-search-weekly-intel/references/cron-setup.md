# Cron Setup

## Recommended mode

Use an isolated cron session so the run stays lightweight and task-focused.

Recommended job shape:
- session target: `isolated`
- delivery: enabled
- channel: Telegram
- destination: the user's chat id
- timezone: user's timezone
- cadence: Sunday evening

## Example add command

Replace the delivery target and adjust the exact time as needed.

```bash
openclaw cron add \
  --name "x-ai-search-weekly-intel" \
  --cron "0 19 * * 0" \
  --tz "Asia/Kolkata" \
  --session isolated \
  --announce \
  --channel telegram \
  --to "telegram:7739622002" \
  --message "Run the x-ai-search-weekly-intel workflow: go to @aisearchio on X, inspect the most recent few posts, pick the recent post that mentions multiple tools/models, research those tools/models across official pages, GitHub, and arXiv, group them by similar use case, write a user-friendly markdown report, render it to PDF, and deliver the PDF plus a short summary here." \
  --timeout-seconds 1800
```

## Notes

- `0 19 * * 0` means Sunday 19:00 in the specified timezone.
- If the workflow becomes browser-heavy, keep the timeout generous.
- If delivery fails often, add `--best-effort-deliver`.
- Use `openclaw cron run <id>` to test manually before trusting the schedule.
- Use `openclaw cron edit <id>` to change time or delivery without recreating the job.
