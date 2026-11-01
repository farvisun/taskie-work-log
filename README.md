# Taskie Work Log

An agent skill that keeps a [Taskie](https://taskie.ir) project up to date with the work your AI agent does.

When the agent starts a job, it finds or creates one task and sets it in progress. When it finishes, it adds a summary comment and marks the task done. Questions that change nothing are not logged.

The default project is «هوش مصنوعی». You can choose a different one.

## Setup

### 1. Install the skill

```bash
npx skills add farvisun/taskie-work-log
```

### 2. Connect your agent to Taskie

In Taskie, open **Settings → Connections & MCP**, click **Connect a client**, and follow the steps for your client. For Claude Code:

```bash
claude mcp add --transport http taskie https://app.taskie.ir/mcp
```

Choose **Full** access when you approve the connection. Read-only connections can't create tasks or comments, and only workspace admins can grant Full access. If you aren't an admin, ask one to set up the connection.

To limit what the agent can reach, select only your logging project under **Advanced settings**. Create the project first, because a connection limited this way can't use any other project.

### 3. Start working

If you have a project named «هوش مصنوعی», the agent uses it. If not, it asks which project to use and remembers your answer.

## Choosing a project

The agent uses the first of these it finds:

1. A project you name in the conversation
2. `.taskie-work-log.json` in the repository root
3. `~/.config/taskie-work-log/config.json`
4. A project named «هوش مصنوعی»

Both files use the same format, and neither holds a token:

```json
{ "project_id": "hash-id-from-taskie", "project_name": "هوش مصنوعی" }
```

## Good to know

- Starting automatically depends on your agent choosing to load the skill, so it can miss a job. For the most reliable logging, add this line to your `CLAUDE.md` or `AGENTS.md`:

  ```markdown
  Before starting any work that changes something, load the taskie-work-log skill and follow it.
  ```

  Saying "log this in Taskie" also works.
- To keep something out of Taskie, tell the agent "don't log this".
- The agent is told to keep secrets and personal data out of tasks, but anyone with access to the project can read what it writes. Use a project with the right members.
- If Taskie is unreachable, the agent tells you once and continues the work.

## راهنمای فارسی

این skill کارهای ایجنت هوش مصنوعی شما را در پروژه‌ای از تسکی ثبت می‌کند. وقتی کاری شروع می‌شود، ایجنت یک تسک پیدا یا ایجاد می‌کند و آن را «در حال انجام» می‌گذارد. در پایان کار، خلاصه را به‌صورت کامنت می‌نویسد و تسک را انجام‌شده می‌کند.

۱. نصب skill:

```bash
npx skills add farvisun/taskie-work-log
```

۲. در تسکی به **تنظیمات ← اتصالات و MCP** بروید، روی اتصال کلاینت کلیک کنید و مراحل کلاینت خود را انجام دهید. موقع تأیید اتصال، دسترسی **کامل** را انتخاب کنید. فقط مدیران فضای کاری می‌توانند این دسترسی را بدهند.

۳. اگر پروژه‌ای با نام «هوش مصنوعی» داشته باشید، ایجنت از همان استفاده می‌کند. در غیر این صورت می‌پرسد کار در کدام پروژه ثبت شود و انتخاب شما را به خاطر می‌سپارد.

## License

[MIT](LICENSE)
