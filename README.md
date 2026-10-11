# LuggageFlow — Warehouse Inventory V1

An Android-friendly, offline-first PWA for tracking luggage warehouse quantities. Built with plain HTML, CSS and JavaScript for editing in Acode.

## Included features
- Dashboard: total units, product variants, low stock, zero stock and recent movements
- Product variants by category, brand, model, material, size and color
- Optional resized product photos
- Smart search by category, brand, model, size, color, location, note and barcode
- Quick Stock In / Stock Out, quantity validation and optional confirmation
- Quick Action Mode queue with pre-save stock validation
- Duplicate variant and barcode prevention
- Low stock and zero stock alerts
- Stock History with safe reversal-based Undo
- Physical Stock Count with adjustment records
- Barcode / QR scanner where the browser supports `BarcodeDetector`, plus manual lookup
- Warehouse rack / shelf location field
- Daily / weekly movement report with CSV export
- JSON backup, basic validation, merge and replace restore
- IndexedDB local data, PWA app-shell cache and light/dark theme
- Data integrity check against movement history

## Open on Android / Acode
1. Download and extract `luggage-warehouse-inventory-v1.zip`.
2. Open the extracted `luggageflow-final` folder in Acode.
3. Open `index.html` to preview the interface. Browser security may restrict service workers and camera access from a local `file://` path.
4. For installable PWA, offline app-shell caching and camera scanning, host the folder on HTTPS (for example GitHub Pages) or serve it through localhost.
5. Open Settings > Backup & Status and export JSON regularly.

## Important data safety notes
- Products and movement history are stored in IndexedDB for the current browser origin on this device. Using another URL can create a separate database.
- Clearing browser/site data or resetting the device can delete local inventory. JSON backup is manual, not cloud sync.
- Export a backup before Restore > Replace. Merge uses record IDs to avoid adding the same IDs twice; it is not a multi-device sync engine.
- Camera scanning requires a secure context (normally HTTPS or localhost), camera permission and a browser with native `BarcodeDetector` support. Manual lookup is always available.
- Barcode / QR IDs are saved per variant, but this version does not render printable QR label images.
- Photos are compressed to a maximum 640px edge and JPEG quality before saving, but many photos can still consume browser storage.
- Undo only reverses a movement when the variant's current stock still equals the movement's recorded after-stock. If later movements changed the stock, use Physical Stock Count to create a safe adjustment.
- A physical count records an adjustment; it does not erase old movements.
- This is a single-device local inventory app. No login, cloud sync, multi-user access, sales, customer or profit module is included in this stock-focused V1.

## Recommended first test
1. Add a test variant with opening stock 10.
2. Stock In 5; expected stock 15.
3. Stock Out 3; expected stock 12.
4. Try Stock Out 99; it should be blocked.
5. Try adding the exact same category / brand / model / material / size / color variant; it should be blocked.
6. Run Data Integrity Check.
7. Export JSON, then test Restore using a copy of the backup.
8. Host on HTTPS, open once online, then test the app shell offline.
