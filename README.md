README
Version 1.0  ·  Single-file web app  ·  Powered by Claude Sonnet
OVERVIEW
ClearLedger is a standalone, single-file HTML web application that uses the Anthropic Claude AI to classify raw bank statement lines into human-readable spending categories. Paste messy transaction text like "POS PUR STARBUCKS #4412" and instantly see a pie chart, summary stats, and a cleaned transaction table — no backend, no install, no database.
HOW IT WORKS  //  THE 3-STEP PIPELINE
STEP A — CLEAN  The AI strips transaction IDs, POS codes, reference numbers, and special characters to extract clean merchant intent from raw statement noise.
STEP B — VECTORIZE  Merchant names are converted into semantic vectors. Words with similar meanings ("SBUX" and "Starbucks") are positioned close together in vector space, enabling fuzzy matching.
STEP C — CLASSIFY  The AI maps each transaction to the nearest category neighborhood: Food & Drink, Groceries, Transport, Entertainment, Shopping, Health & Fitness, Travel, or Other.
GETTING STARTED
1.  Open  txn-classifier.html  in any modern web browser (Chrome, Firefox, Safari, Edge).
2.  Click "load sample →" to populate the input with 20 realistic messy transactions.
3.  Click "Classify Transactions" — the AI processes and returns results in seconds.
4.  View your spending donut chart, category legend, and cleaned transaction table.
5.  Paste your own bank export lines and repeat.
REQUIREMENTS
Browser	Any modern browser with ES6+ support. No extensions needed.
API Key	An Anthropic API key is required. The app calls api.anthropic.com directly from the browser.
Internet	Required to load Google Fonts and contact the Anthropic API.
Backend	None. This is a fully client-side application.
Install	None. Just open the .html file.

API KEY SETUP
The app calls the Anthropic API directly from your browser. Because this is a client-side app, you will need to inject your API key. Open txn-classifier.html in a text editor and locate the fetch() call to api.anthropic.com. Add your key to the headers object:
headers: {
  "Content-Type": "application/json",
  "x-api-key": "sk-ant-YOUR_KEY_HERE",
  "anthropic-version": "2023-06-01"
}
Note: For production use, never expose API keys in client-side code. Use a backend proxy instead.
SPENDING CATEGORIES
Food & Drink	Restaurants, cafes, coffee shops, fast food
Groceries	Supermarkets, food stores, farmers markets
Transport	Ride-share, fuel, parking, public transit
Entertainment	Streaming, gaming, cinema, subscriptions
Shopping	Retail, e-commerce, clothing, general goods
Health & Fitness	Pharmacy, gym, medical, wellness
Travel	Flights, hotels, vacation rentals, car hire
Other	Anything that does not fit the above

FILE STRUCTURE
txn-classifier.html
├── <nav>          Navigation bar with logo and badge
├── <section>      Hero landing section with CTA
├── <section>      "How It Works" — 3-step pipeline cards
├── <div#app>      Classifier terminal UI
│   ├── textarea   Raw transaction input
│   ├── button     Classify trigger → Anthropic API call
│   └── #results   Stats, donut chart, and table (rendered dynamically)
└── <footer>       Credit and privacy note

External dependencies (CDN):
  · Chart.js 4.4.1      (donut chart)
  · Google Fonts         (IBM Plex Mono, Syne)
  · Anthropic API        (classification AI)
PRIVACY & SECURITY

·  Transaction data is sent to Anthropic's API for classification and is subject to Anthropic's privacy policy.
·  No transaction data is stored locally (no localStorage, no cookies, no server).
·  The app runs entirely in your browser — there is no backend server involved.
·  Do not paste full account numbers, card numbers, or passwords into the input field.
·  For sensitive financial data, consider running this behind a proxy server with server-side API calls.
CUSTOMISATION
Add categories:  Edit the CAT_COLORS and CAT_EMOJI objects in the <script> block and update the AI prompt.
Change the model:  Replace "claude-sonnet-4-20250514" with any supported Anthropic model string.
Adjust max_tokens:  Increase max_tokens in the API call body if classifying more than ~50 transactions.
Change currency:  The app parses the $ symbol by default. Update the regex in renderResults() for other currencies.

