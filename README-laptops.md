# TechSupport Laptops Page

A product discovery and lead page (`laptops.html`). The existing `index.html` enquiry page is untouched.

## Files created
| File | Purpose |
|---|---|
| `laptops.html` | The page (nav, hero, products, why us, about, contact, footer) |
| `assets/laptops.css` | Styling |
| `assets/laptops.js` | Renders cards, fills the product field, validates, submits |
| `assets/products-data.js` | **All product information** |
| `api/enquiry.js` | Server-side route that forwards the enquiry to Make |
| `.env.example` | Names the environment variable |

The existing project is a plain static site, so this uses plain HTML, CSS and JavaScript, plus a Vercel serverless function for the API route.

## Editing products
Open `assets/products-data.js`. Change `name`, `category`, `description`, `processor`, `ram`, `storage`, `screen` and `price` (a number in Naira). To add a real photo, put it in `assets/img/` and set `image: "assets/img/your-file.jpg"`. With `image: ""` a placeholder illustration is shown. Add or remove entries and the cards and the form dropdown update automatically.

## Make webhook
The browser only calls `/api/enquiry`. That function reads the webhook from the environment variable `MAKE_WEBHOOK_URL`. In Vercel: Project Settings, Environment Variables, add `MAKE_WEBHOOK_URL` with your Make webhook URL, then redeploy. For local testing, copy `.env.example` to `.env.local`, fill it in and run `npx vercel dev`. If the variable is missing, the form shows a configuration error and nothing is sent.

## JSON sent to Make
```json
{
  "Customer Name": "", "Email": "", "Phone": "", "Product Interested In": "",
  "Budget": "", "Customer Message": "",
  "Lead Source": "Product Page", "Submission Date": "2026-11-16T10:00:00.000Z"
}
```
`Submission Date` is an ISO timestamp (UTC) created on the server.

## Testing
1. In Make, create a scenario with a Custom webhook, click **Run once**, then run `npx vercel dev`.
2. Open `/laptops.html`, click **Enquire About This Laptop** and confirm the product is pre-selected.
3. Submit empty to see validation, then submit valid details and confirm Make receives the fields above.
4. Remove `MAKE_WEBHOOK_URL`, submit again and confirm a configuration error is shown.
5. Double-click Send and confirm only one request is made.

## Still to do
- Set `MAKE_WEBHOOK_URL` in Vercel.
- Replace the placeholder email and phone in `laptops.html` (contact section and footer).
- Confirm real specifications and prices, and add real product photos.
- Link to this page from your site, and optionally link the existing enquiry page.
