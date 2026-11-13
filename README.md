# Daily Timetable (n8n Workflow)

A simple, no-code n8n workflow that shows your timetable for **today**, sorted by time. No API keys, no coding, no external accounts needed.

## How It Works

1. **Daily 07:00 Trigger** (Schedule Trigger): runs every morning at 7:00 AM. A second **Test Manually** trigger lets you run it any time.
2. **Get Today Tasks** (Data Table): fetches only today's rows, matched by weekday number (Monday = 1 ... Sunday = 7).
3. **Sort By Start Time** (Sort): orders the tasks from earliest to latest.
4. **Format Schedule Line** (Edit Fields): builds a clean line for each task, like `08:00 - 10:00 | Study: English`.

```
Daily 07:00 Trigger ─┐
                     ├─> Get Today Tasks ─> Sort By Start Time ─> Format Schedule Line
Test Manually ───────┘
```

## Timetable Data

The timetable is stored in an n8n **Data Table** named `Timetable` with these columns:

| Column       | Type   | Example            |
|--------------|--------|--------------------|
| `day`        | string | Friday             |
| `day_number` | number | 5                  |
| `start_time` | string | 08:00              |
| `end_time`   | string | 10:00              |
| `task`       | string | Study: English     |

Use 24-hour time (`HH:MM`) so sorting works correctly. To change your timetable, open the Data Table in n8n and add, edit, or delete rows. No code is needed.

## Setup

1. Open your n8n instance and create a new workflow.
2. Add the nodes listed above, or import the workflow if you have exported it as JSON.
3. Create a Data Table called `Timetable` with the columns shown above and add your rows.
4. In **Get Today Tasks**, select your `Timetable` table and filter `day_number` equals `{{ $now.weekday }}`.
5. Click **Test Manually** to check the output.
6. Publish the workflow so the 07:00 schedule starts running.

## Timezone

n8n uses the workflow timezone for the schedule and for `$now`. If your times look off, set the timezone in **Workflow Settings** (for example `Asia/Karachi`).

## Possible Extensions

- Send the daily schedule to Telegram, Gmail, or WhatsApp (needs you to connect that account in n8n).
- Read the timetable from Google Sheets instead of the Data Table.
- Write today's schedule into a "Today" tab in Google Sheets.

## Requirements

- An n8n instance (cloud or self-hosted) with Data Tables available.

## License

MITC
