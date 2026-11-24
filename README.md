# Soap-saa | Online Soap Store (2 SKUs)

## Included
- `index.html`: responsive Soap-saa landing page, product cards, cart and checkout form.
- `admin.html`: order dashboard, pick/pack checklist, status and tracking updates, printable packing slip + address label.
- `assets/`: Honey Oat and Aloe Vera product artwork.
- `products.csv`: importable 2-SKU product list.
- `gas-backend/Code.gs`: Google Apps Script API for products, order intake, stock deduction and admin order updates.

## Google Sheets setup
1. Upload `Soap-saa_Google_Sheets_Template.xlsx` to Google Drive and open it with Google Sheets (or create a blank Google Sheet).
2. In the Sheet: Extensions → Apps Script. Paste `gas-backend/Code.gs`.
3. Change `ADMIN_PIN` to a private value.
4. Run `setup()` once and authorize. The script creates Products, Orders and OrderItems tabs and inserts the two sample SKUs when Products is empty.
5. Deploy → New deployment → Web app. Execute as: Me. Access: Anyone. Copy the deployment URL.
6. Paste that URL into `API_URL` in both `app.js` and `admin.html`.
7. Commit/push the updated files to GitHub, then redeploy on Vercel.

## GitHub + Vercel
- Upload all files and the `assets` folder to repository `baan-soap` (or your preferred repo).
- Vercel project settings: Framework Preset `Other`, Build Command blank, Output Directory `.`.
- Deploy. Open `/` for the storefront and `/admin.html` for fulfillment.

## Fulfillment workflow
1. Customer checks out; Apps Script writes Orders and OrderItems and deducts stock in Products.
2. Admin opens `/admin.html`, enters the private PIN and loads orders.
3. Pick products, set status to `กำลังแพ็ค`, update carrier/tracking, and print the packing slip/address label.
4. Mark `พร้อมจัดส่ง` or `จัดส่งแล้ว` after handing over to the carrier.

## Important limitations
- Printed address label is a shop-generated label/packing slip, not an official carrier label. Official carrier labels and pickup booking require a courier API/account integration.
- Do not use real customer data until you have tested the Apps Script permissions and deployment.
- For security, use a strong admin PIN and do not share it publicly. Consider moving admin access to authenticated accounts for a production store.
