# Homekeep

**AI-powered tracker for device maintenance, warranties and subscription renewals.**
Scan a bill to identify the product and model, then renew or book service on the maker's official site.

![license](https://img.shields.io/badge/license-MIT-0C6B5D) ![build](https://img.shields.io/badge/build-none-lightgrey) ![stack](https://img.shields.io/badge/stack-HTML%20%7C%20CSS%20%7C%20JS-13212B)

---

## Why

Warranties lapse, yearly services get forgotten and subscriptions renew quietly. Homekeep keeps every date in one place and sends you to the right official page when action is due.

## Features

| Area | What it does |
|---|---|
| **Bill scanner** | Upload a photo or screenshot of a bill. AI reads product, brand, model number, serial, purchase date, price, warranty, plan and billing cycle. You review and save. |
| **Devices** | Yearly (or custom) service due dates, warranty end dates, last service, mark as serviced. |
| **Subscriptions** | Netflix, Spotify, Google One, Prime, YouTube, Hotstar, Apple, Microsoft and more. Renewal dates, billing cycle, monthly cost total, mark as renewed. |
| **Official links** | One button per item opens the company's own service or account page in a new tab. Unknown brands get a "Find official site" search. You can set your own https link. |
| **Overview** | Overdue items, items due in 30 days and a 60-day timeline on the first screen. |
| **Themes and layout** | Light and dark themes, works from phone width up. |

## Supported brands for official links

- **Subscriptions:** Netflix, Spotify, YouTube, Google One, Amazon Prime, Hotstar, SonyLIV, ZEE5, Apple, iCloud, Microsoft, Adobe.
- **Devices:** Samsung, LG, Apple, Sony, Dell, HP, Lenovo, Asus, Acer, Xiaomi, Redmi, OnePlus, Realme, Panasonic, Whirlpool, Bosch, Canon, Daikin, Voltas, Godrej, Haier.

Missing yours? See [CONTRIBUTING.md](CONTRIBUTING.md). It is a one-line change.

## Quick start

No build step and no dependencies.

```bash
git clone https://github.com/<your-username>/homekeep.git
cd homekeep
python3 -m http.server 8080
# open http://localhost:8080
```

You can also open `index.html` directly, or host the folder on GitHub Pages (Settings, Pages, deploy from the `main` branch root).

## Important: where AI bill scanning works

Bill scanning, and syncing items to an account, use the runtime of the Claude artifact viewer (`sample`, `db` and `user` capabilities). That means:

| Where you run it | Bill scanning | Account sync | Manual entry, dates, links |
|---|---|---|---|
| Published as a Claude artifact | Yes | Yes | Yes |
| GitHub Pages, localhost or any other host | No (button is disabled with a message) | No | Yes, stored in your browser |

To enable scanning on your own host, replace `readBill()` in `index.html` with a call to a vision-capable model API that returns the JSON shape described in [docs/how-bill-scanning-works.md](docs/how-bill-scanning-works.md). Keep API keys on a server, never in the page.

## How dates are worked out

- **Next service** = last service date (or purchase date if never serviced) plus the service interval in months.
- **Warranty end** = purchase date plus warranty months.
- **Subscription renewal** = the renewal date you enter. "Mark renewed" moves it forward by one billing cycle.
- **Monthly cost** = price divided by months in the billing cycle, summed over subscriptions.

## Privacy

- Items live in your browser's `localStorage`, plus a private per-user store when signed in to Claude.
- A bill image is sent to Claude only when you press "Read bill" and have allowed it.
- No analytics, no trackers, no other servers.
- Always check the address bar shows the brand's real domain before signing in or paying.

## Project structure

```
homekeep/
├── index.html                      # the whole app (HTML, CSS, JS)
├── docs/
│   └── how-bill-scanning-works.md
├── .github/ISSUE_TEMPLATE/         # broken-link and feature templates
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## Roadmap

- [ ] Email or push reminders before due dates
- [ ] Add to calendar (.ics export)
- [ ] PDF bill support
- [ ] Multiple warranty and AMC records per device
- [ ] Per-person or per-household sharing
- [ ] More brands and regions

## Contributing

Pull requests are welcome, especially new brand links and fixes to dead ones. Read [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)

---

Homekeep is not affiliated with any brand named above. Brand names are used only to link to each company's own website.
