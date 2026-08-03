# Odprawa — Customs Clearance Composer
### User Manual (v1)

This tool helps you turn a shipment invoice into the formatted Polish email you send back to FedEx (`pl-import@fedex.com`) or DHL (`odprawacelna@dhl.com`). It does **not** send email for you — it prepares the text, you copy it into Gmail and send it yourself, same as today.

---

## 1. Opening the app

Open the `customs-clearance-composer.html` file in any browser (Chrome, Edge, etc.) — double-click it, or drag it into a browser window. No install, no login. It works fully offline except for two small one-time downloads the browser fetches automatically the first time you open it (the PDF-reading and handwriting-recognition libraries) — you need internet the first time, not after.

---

## 2. The three shipment types (top-left tabs)

Pick the tab that matches the shipment you're working on:

| Tab | Use for |
|---|---|
| **Bangkok** | Diacrown Co. Ltd (Bangkok) gemstone shipments via FedEx |
| **India** | DIACROWN (Bharat Diamond Bourse, Mumbai) shipments via FedEx — often split across 2–3 invoices |
| **Elegant Coll.** | Elegant Collection jewelry shipments via DHL |

The tab you pick changes: which columns the item table shows, which boilerplate text gets used, and which parser the app tries first when reading an attachment.

---

## 3. Invoice source

Just under the tabs, pick where the invoice came from:

- **Our own invoice** — no courier reply address shown (nothing to reply to yet)
- **FedEx invoice / AWB** — shows `pl-import@fedex.com` as the reply address
- **DHL invoice** — shows `odprawacelna@dhl.com` as the reply address

This is just a label/reminder — it doesn't send anything, it just reminds you who the final email goes to.

---

## 4. Reading the attachment automatically

This is the main time-saver. Under **"Read from attachment"**:

1. Click the box (or drag a file onto it) and choose the invoice PDF or image you received.
2. The app reads it automatically:
   - If it's a normal digital PDF, it reads the text directly.
   - If it looks scanned (a photo or scanned document with no selectable text), it runs OCR automatically — this takes a bit longer.
3. Click **"Parse rows from text →"**. The app tries to recognize the invoice as one of the three known layouts (Bangkok / India / Elegant Collection) and fills in the item table for you.
4. **Always check the table before generating the email.** The status line under the upload box tells you how confident the result is:
   - *"Parsed from the recognized invoice layout"* (green) — matched a known format, still worth a glance.
   - *"Parsed with the generic guesser"* (amber) — the app didn't recognize the exact layout and took its best guess at the numbers. Review every row carefully.
   - *"Couldn't confidently detect rows"* — add the rows manually (see Section 7).

You can always expand **"Raw extracted text"** underneath to see exactly what the app read from the file, which is useful if a row looks wrong and you want to see the original wording.

**A note on accuracy:** some digital PDFs store their text out of visual order internally (depends on what software made the PDF) — when that happens, extraction can come out jumbled even though the file isn't scanned. If a parse looks scrambled, check "Raw extracted text" — if that's already jumbled, the source PDF is the issue, not the parser. Send me a copy and I can look at tuning around it.

---

## 5. Value reconciliation

Shown for every shipment type, since our invoice total needs to match the courier's declared total across all three flows, not just India.

- If you upload and parse the courier's document (AWB/manifest), the **courier total** field fills in automatically.
- If you upload and parse our invoice, the **our invoice total** field fills in automatically.
- The app tells you immediately whether they match (green ✓) or not (amber ⚠, with the dollar difference). India is where this comes up most often — FedEx frequently attaches only one of 2–3 invoices — but it's worth checking on Bangkok and Elegant Collection too. If there's a mismatch, use the notes field (Section 6) to record why, or correct the figures once you've tracked down the missing document.

---

## 6. Notes, remarks, and sign-off

- **Additional notes / remarks** — optional free text, e.g. explaining a value discrepancy. If filled in, it's inserted into the email just before the closing line.
- **Your name** — defaults to "Weronika Byczenko"; change it if someone else is sending. This becomes the sign-off name in the generated email.

---

## 7. The item table

Whether parsed automatically or not, every row is editable:

- Click any cell to type or correct it.
- **+ Add row** adds a blank row.
- The **×** button on the right of a row deletes it.
- **Auto-translate descriptions** runs the English→Polish dictionary over every description cell. Anything it doesn't recognize is shown in red with a small warning underneath — translate those manually, since the dictionary only knows terms seen so far (extend it any time by sending me new terms).
- The bottom row updates automatically with totals (quantity and price summed; for Elegant Collection, weight too).
- **Elegant Collection only:** two extra fields appear below the table for **shipping cost** and **insurance**, which get added into the final total.

---

## 8. Package contents line

For Bangkok and India, choose whether the shipment contains:
- Precious & semi-precious (default)
- Precious only
- Semi-precious only

This picks the correct fixed sentence for the email (matches the actual template wording exactly). Elegant Collection doesn't use this — its contents line is built automatically from the item descriptions instead.

---

## 9. Canned responses

Two checkboxes let you drop in a pre-written, already-approved reply instead of typing it:

- **GIA/carat pushback** — the standard pushback when a customs agent asks for a certificate and carat weight for every individual stone.
- **Missing invoice note** (India only) — the standard explanation when you're attaching a previously-missing invoice to resolve a value mismatch.

Check the box before clicking Generate if you want it included; leave both unchecked for a normal reply.

---

## 10. Generating and sending

1. Click **Generate email text**. The output box fills with the complete Polish email — importer details, contents line, procedure lines, the item table, totals, any remarks, and sign-off — in the same order as the approved template.
2. Click **Copy to clipboard**.
3. Open Gmail, reply in the correct thread (to the courier address shown in Section 3), paste, do a final read-through, and click Send — same last step as always.

The app never sends anything itself — step 3 is still a manual, deliberate action on your part.

---

## Quick troubleshooting

| Problem | What to do |
|---|---|
| Upload says "Couldn't read that file" | Try a different export of the PDF, or fall back to manual entry (Section 7) |
| Parsed rows look wrong or jumbled | Check "Raw extracted text" — if it's already jumbled there, it's how the source PDF stores its text, not a parsing bug; fix the table by hand |
| A description won't auto-translate | It's not in the dictionary yet — translate it manually and let me know the term so I can add it |
| Totals look off | They're computed live from whatever's currently in the table — double check qty/price in each row |
| Values don't match the courier's total | Use Section 5's reconciliation check, then explain the difference in the Notes field (Section 6) |

---

## Advanced features (v2)

**Translate any English text to Polish (draft).** Two ways:
- In the Line items table, click **"Translate unmatched (draft)"** — it sends only the rows flagged red (no dictionary match) to a translation service and fills in a Polish draft, marked with an amber "machine-translated draft — verify wording" note. Always double-check these against your actual terminology before sending.
- The new **"Quick phrase translator"** panel (left column) takes any English text — a sentence, an agent's question, anything not covered by the fixed templates — and gives you a Polish draft, with a one-click button to drop it straight into the Notes/remarks field.

Both require an internet connection and are drafts only, never applied automatically to anything you haven't asked to translate.

**Duplicate row (⧉ icon).** Next to each row's delete (×) button — copies that row directly below it, useful when several items share the same material/weight pattern and only one field differs.

**Readiness checklist.** Above the Generate button — shows at a glance whether line items are present, contents are filled in (Elegant Collection), values are reconciled, and the signer name is set, so a Generate attempt is less likely to come out incomplete.

**Download as .txt.** Saves the generated email to a file, in case you want to keep a copy outside of Gmail or hand it to someone else.

**Reset form.** Clears everything and starts fresh — asks for confirmation first since it can't be undone.
