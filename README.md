# Jeremiah's Auto — "Sell My Car" (Prototype)

A standalone demo, completely separate from the inventory system. Open `sell-my-car.html` in any browser — nothing to install, works on phone, tablet, or laptop.

## The idea in one line

A public "Sell My Car" page for anyone to submit their vehicle for assessment, and a private admin screen — on the same page, but genuinely walled off — where only Jeremiah's Auto can see submissions and respond over WhatsApp.

## Walking through the demo

**As a seller:**
1. Land on the page, click **Sell My Car**
2. Fill in the vehicle details, add at least 3 photos, add your name and number
3. Submit — takes about two to three minutes, exactly as briefed
4. Get a confirmation with a reference number (a "ticket," styled like a valuation stub — e.g. **#1041**)

**As the admin (your client):**
1. Click the small **Admin** link, top-right of the page
2. Enter the demo passcode: **1234**
3. See every submission in one list — reference number, seller name, car, and a status tag
4. Click into any one to see the full form and photos
5. Click **Message on WhatsApp** — opens a real WhatsApp chat, pre-filled with a message referencing that seller's car and reference number
6. Update the status (New → Contacted → Offer Made → Purchased → Declined) as the deal progresses

## What's new in this round

**Software fixes:**
- Every form label is now properly linked to its field — tapping the label text focuses the field, which matters most on phones
- Adding photos now hints mobile browsers to open the camera directly, since most sellers will be standing next to the car
- Year and mileage now have real, enforced limits (year 1980–2027, mileage 0–900,000 km) — typing something outside that range blocks submission with a clear message, not just a cosmetic restriction
- Clicking any photo in the admin view opens it full-size in a lightbox, so assessing a car's condition doesn't mean squinting at a tiny thumbnail
- The admin list now has a search box (by name, make, or model) and a status filter — built for when this has 50 submissions, not just 2

**Marketing/trust additions (see the table below for what's placeholder vs. needs a real decision):**
- Two accreditation badges (RMI, NCR) on the landing page
- A phone number and email in the footer
- A privacy reassurance line right where personal details are collected
- Footer links (Privacy Policy, Terms, Contact Us)

**Deliberately left out for now, per your call:**
- Testimonials — waiting on real quotes, since invented ones would undermine the trust this page is trying to build
- A way for a seller to check back on their own submission's status — worth discussing with your client first, since it changes the technical shape of the reference number system

## Mobile, tablet, and laptop — actually tested, not assumed

Before this went back to you, it was tested on real simulated devices using an actual browser engine (not just checked by reading the code): iPhone SE, iPhone 14, a narrow Android phone, an iPad, and a laptop. On each one, the test checked for things a person would actually notice — nothing spilling off the edge of the screen, every button big enough to comfortably tap with a thumb, and the whole submission flow (including a real photo upload, not a placeholder) working start to finish.

Two real issues turned up and were fixed:
- The photo upload button was a few pixels short of a comfortable tap target on phones — made it bigger
- The real photo-resizing pipeline (which compresses large phone photos down before storing them) had never actually been verified end-to-end before, since the testing tools used earlier in this project couldn't fully simulate a real photo upload. This time, real test photos (up to 1600×1200) were uploaded through an actual browser, and confirmed to resize down correctly, display correctly in both the form and the admin view, and open correctly in the photo lightbox.

## Deploying this to GitHub Pages

This file is ready to deploy as-is — it's a single self-contained HTML file with no server requirements, so GitHub Pages (which only hosts static files) is a good fit.

1. Create a new repository on GitHub (can be named anything, e.g. `jeremiahs-auto-sell-my-car`)
2. Upload `sell-my-car.html` into it — for the simplest URL, rename it to `index.html` when you upload (otherwise your link will need `/sell-my-car.html` on the end)
3. In the repository, go to **Settings → Pages**, and under "Source" choose the branch you uploaded to (usually `main`) and the root folder
4. GitHub will give you a live URL, typically `https://yourusername.github.io/repository-name/` — that's what you send your client

One thing worth knowing: once it's on a real URL like that, the "saves your submissions" behavior becomes tied to *that specific web address* — so if you later move it to a different URL or a custom domain, submissions made on the old address won't carry over. That's normal, expected behavior for how browsers store data, not a bug — just worth knowing if you end up testing on the GitHub Pages link and expect to see the same data as your local file.

## Being upfront about what's real and what's a placeholder

| Piece | Status |
|---|---|
| The full submission form, validation, and flow | **Fully real** — try breaking it, it's built to hold up |
| Reference number generation | **Fully real** — increments correctly, never collides, even after a refresh |
| Photos | **Fully real now.** Actual photos are captured, resized down in the browser (so real phone photos don't overwhelm storage), and genuinely displayed as real thumbnails — both in the form and in the admin view. Verified by testing actual image resizing math, not just that a filename shows up |
| Saving submissions | **Fully real now, within this browser.** Submit a car, close the tab or refresh the page, and it's still there — reference number, details, and photos included. This was specifically tested by simulating a full page reload and confirming everything survives intact |
| Admin list and detail view | **Fully real** — pulls from actual submitted data |
| WhatsApp button | **Fully real and tested** — correctly converts a local South African number (e.g. `082 123 4567`) into the international format WhatsApp actually requires to open a chat. This was checked carefully, since a wrong number format here would mean the one button that matters most silently doesn't work |
| Status tracking | **Fully real**, and now saved — a status change survives a refresh too |
| Data storage | **Saved to this browser only.** It lives in this specific browser, on this specific device — not shared with any other device, browser, or person. Real use across multiple staff or devices needs a backend |
| The admin passcode ("1234") | **Placeholder, not real security.** It shows the *idea* of a restricted area, but anyone who looks at the page's source code can see it. A real build needs proper staff logins enforced by a backend, not a password typed into the front end |
| The privacy promise itself | **Not yet actually enforced.** The whole point of this feature — one seller can never see another seller's submission — currently works only because there's no interface for a seller to browse anything else. True privacy needs to be enforced at the data layer (a backend rule saying "you can submit, but never read anyone's data back"), the same way we discussed for the inventory system's cost/profit access. This is the single most important thing to get right before this goes live for real |
| RMI / NCR badges | **Demo placeholders, clearly labeled "(demo)" on the page itself.** You mentioned he likely holds these accreditations for real — if so, swap these for the genuine badges/logos once confirmed. If not, remove them; claiming an accreditation the business doesn't hold is a real legal risk, not just a style choice |
| Phone number and email in the footer | **Intentionally, completely fake.** The phone number is an obviously placeholder sequence, and the email uses the `.example` domain — a domain reserved by internet standards that can never actually be registered or receive mail, so there's no risk of a real inbox getting contacted by mistake. Replace both with real ones whenever this moves toward production |
| Footer links (Privacy Policy, Terms, Contact Us) | **Placeholder only** — they're visually present but don't go anywhere yet. Real policies need real legal content behind them |

## Why this is a separate file from the inventory system

You asked for these to stay independent for now, so this has zero connection to `index.html` — different file, different code, nothing shared. If your client wants both, they'd eventually share one real backend (which is efficient — one login system, one database, two connected tools) but that's a conversation for after he's decided what he wants, not something built into this demo.

## A design note

This uses Jeremiah's Auto's red and black, plus a warm gold accent for a premium, valuation-certificate feel — deliberately different from the internal inventory tool's look, since this one's job is to make a stranger on the internet trust the business enough to hand over their car details, not help staff move fast through daily tasks. Same company, same colors at the core, different job, different feel.

## If you want to reset the demo before showing it again

Since submissions now save in the browser, test entries you create while rehearsing will still be there next time you open the file. To start fresh: open the browser's developer tools (F12), go to the Console tab, and run:

```
localStorage.clear()
```

Then refresh the page. Everything goes back to empty, ready for a clean demo.
