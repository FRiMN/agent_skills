---
name: gccli
description: Google Calendar CLI for listing calendars, viewing/creating/updating events, and checking availability.
---

# Google Calendar CLI

Command-line interface for Google Calendar operations.

## Installation

```bash
npm install -g @mariozechner/gccli
```

## Setup

### Google Cloud Console (one-time)

1. [Create a new project](https://console.cloud.google.com/projectcreate) (or select existing)
2. [Enable the Google Calendar API](https://console.cloud.google.com/apis/api/calendar-json.googleapis.com)
3. [Set app name](https://console.cloud.google.com/auth/branding) in OAuth branding
4. [Add test users](https://console.cloud.google.com/auth/audience) (all Gmail addresses you want to use)
5. [Create OAuth client](https://console.cloud.google.com/auth/clients):
   - Click "Create Client"
   - Application type: "Desktop app"
   - Download the JSON file

### Configure gccli

First check if already configured:
```bash
gccli accounts list
```

If no accounts, guide the user through setup:
1. Ask if they have a Google Cloud project with Calendar API enabled
2. If not, walk them through the Google Cloud Console steps above
3. Have them download the OAuth credentials JSON
4. Run: `gccli accounts credentials ~/path/to/credentials.json`
5. Run: `gccli accounts add <email>` (use `--manual` for browserless OAuth)

If the OAuth consent screen uses user type External with publishing status Testing, the refresh token expires after 7 days. Re-run `accounts add` when calls start failing with `invalid_grant`, or publish the app (In production) to remove the limit.

## Usage

Run `gccli --help` for full command reference.

Common operations:
- `gccli <email> calendars` - List all calendars
- `gccli <email> events <calendarId> [--from <dt>] [--to <dt>]` - List events
- `gccli <email> event <calendarId> <eventId>` - Get event details
- `gccli <email> create <calendarId> --summary <s> --start <dt> --end <dt>` - Create event
- `gccli <email> freebusy <calendarIds> --from <dt> --to <dt>` - Check availability

Use `primary` as calendarId for the main calendar.

## Date/Time Format

- Timed events: `YYYY-MM-DDTHH:MM:SSZ` (UTC) or an explicit offset such as `YYYY-MM-DDTHH:MM:SS+07:00`.
- A bare local time without a zone (`YYYY-MM-DDTHH:MM:SS`) is rejected by the Calendar API: `Error: Missing time zone definition for start time.` Always pass `Z` or an offset.
- Output of `events` / `event` is rendered in the machine's local timezone with its offset (e.g. `2026-11-17T10:00:00+07:00`).
- All-day events: `YYYY-MM-DD` with `--all-day` flag

## Behavior Notes

- `delete` is a soft delete: it prints `Deleted` and the event disappears from `events` lists, but `event <calendarId> <eventId>` still returns the record with `Status: cancelled`. This is expected, not a failed delete.
- An API call may occasionally hang without any output; retry it or wrap invocations in `timeout 30`. A retry normally succeeds immediately.

## Data Storage

- `~/.gccli/credentials.json` - OAuth client credentials
- `~/.gccli/accounts.json` - Account tokens
