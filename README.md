# BrokenShells events

Public news & events feed for the BrokenShells website (ethical hacking team, IEEE Student Branch of Volos).

The website reads [`events.json`](events.json) straight from GitHub:

```
https://raw.githubusercontent.com/brokenshells/events/main/events.json
```

## Adding or changing an event

1. Open `events.json` on GitHub and click the pencil (edit) icon.
2. Add an object to `items` (copy an existing one), then commit to `main`.
3. The site picks it up within about 5 minutes (GitHub caches raw files). No rebuild needed.

Only team maintainers can push. A typo that breaks the JSON makes the site show
"Could not reach the feed", so check the commas and quotes before committing.

## Format

```json
{
	"items": [
		{
			"id": "htb-meetup-volos-2026-10",
			"kind": "event",
			"date": "2026-10-17T18:00:00+03:00",
			"end": "2026-10-17T21:00:00+03:00",
			"title": { "en": "HTB Meetup Volos", "el": "HTB Meetup Βόλου" },
			"summary": { "en": "...", "el": "..." },
			"location": { "en": "ECE Department", "el": "Τμήμα ΗΜΜΥ" },
			"url": "https://www.meetup.com/hack-the-box-meetup-volos-gr/",
			"tags": ["htb", "meetup"]
		}
	]
}
```

| Field      | Required | Notes |
| ---------- | -------- | ----- |
| `id`       | yes      | Unique, any text. |
| `date`     | yes      | `2026-10-17T18:00:00+03:00` (with time; `+03:00` in summer, `+02:00` in winter) or `2026-10-08` for an all-day item. |
| `title`    | yes      | Text or `{ "en": "...", "el": "..." }`. Missing Greek falls back to English. |
| `kind`     | no       | `"event"` (default) or `"news"`. |
| `end`      | no       | Same format as `date`. |
| `summary`  | no       | Text or `{ "en", "el" }`. |
| `location` | no       | Text or `{ "en", "el" }`. |
| `url`      | no       | Must start with `https://` or `http://`. Shown as a "Details" link. |
| `tags`     | no       | Up to 4 are shown. |

Events stay under "Upcoming" until they end (all-day events until midnight), then move to the archive.
News items always go to the archive. Items with missing or invalid required fields are skipped.
