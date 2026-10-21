# How bill scanning works

1. The user picks a JPG, PNG, WebP or GIF of a bill or receipt.
2. The page sends the image and a fixed instruction to Claude through the `sample` capability of the Claude artifact runtime (`sample.json(prompt, { images })`).
3. Claude returns one JSON object: kind (device or subscription), name, brand, model, serial, purchase date, price, currency, warranty months, plan, billing cycle, next renewal date and a confidence level.
4. The page validates dates and numbers and fills the form. Nothing is saved until the user checks the fields and presses Save.

## Rules baked into the prompt

- Copy model and serial numbers exactly as printed. Never guess.
- Use an empty value for anything not on the bill.
- If a subscription bill has no renewal date, the page estimates one from the purchase date and billing cycle, and the user can correct it.

## Privacy

- The image is sent to Claude on the viewer's own Claude account, only after the viewer allows it.
- Items are stored in the browser (`localStorage`) and, when signed in to Claude, in the artifact's private per-user store.
- No data is sent to any other server.

## Running it outside Claude

The `sample`, `db` and `user` capabilities exist only inside the Claude artifact viewer. Elsewhere the app hides bill scanning and works as a manual tracker. To scan bills on your own host, replace the `readBill()` function with a call to a vision model of your choice that returns the same JSON shape.
