# Twenty CRM - LinkedIn Capture Extension

A Chrome extension to capture LinkedIn profiles and companies directly into your self-hosted Twenty CRM instance.

## Features

- **LinkedIn Profile Capture**: Extracts name, headline, company, location, and profile image from LinkedIn profiles
- **Company Page Capture**: Extracts company name, website, industry, employee count, and logo
- **Duplicate Detection**: Checks if the person/company already exists in your CRM before creating
- **Quick Access**: Shows "Open in Twenty" button for existing records
- **Session-Based Auth**: Uses your existing Twenty login session (no API key needed)
- **Recent Captures**: View your recently captured profiles in the popup

## Installation

### Development Mode

1. Install dependencies:
   ```bash
   npm install
   ```

2. Build the extension:
   ```bash
   npm run build
   ```

3. Load in Chrome:
   - Open `chrome://extensions/`
   - Enable "Developer mode"
   - Click "Load unpacked"
   - Select the `.output/chrome-mv3` folder

### Development with Hot Reload

```bash
npm run dev
```

This starts the extension in development mode with automatic reloading.

## Usage

1. **Configure Twenty URL**: Click the extension icon and enter your Twenty CRM URL (e.g., `https://crm.yourdomain.com`)

2. **Log in to Twenty**: Make sure you're logged into your Twenty instance in the same browser

3. **Visit LinkedIn**: Go to any LinkedIn profile (`/in/...`) or company page (`/company/...`)

4. **Capture**: Click the floating button in the bottom-right corner:
   - **"Add to Twenty"**: Creates a new record in your CRM
   - **"Open in Twenty"**: The record already exists - click to view it

## How It Works

The extension reads your Twenty session cookie (`tokenPair`) to authenticate API requests. This means:
- No need to manage API keys
- Uses your existing permissions
- Automatically logs out when your Twenty session expires

## Project Structure

```
twenty-crm-extension/
├── entrypoints/
│   ├── background.ts     # Service worker for API calls & cookie handling
│   ├── content.ts        # LinkedIn page injection & floating button
│   └── popup/            # Extension popup UI
├── utils/
│   ├── linkedin-scraper.ts  # DOM scraping for LinkedIn data
│   ├── twenty-api.ts        # GraphQL client for Twenty API
│   └── storage.ts           # WXT storage utilities
├── types/
│   └── index.ts          # TypeScript type definitions
└── wxt.config.ts         # WXT configuration
```

## Permissions

The extension requires:
- `storage`: Save settings and recent captures
- `cookies`: Read Twenty session token
- `activeTab`: Access current tab URL
- `host_permissions`: Access LinkedIn and your Twenty instance

## Building for Production

```bash
npm run build
npm run zip  # Creates a .zip file for distribution
```

## Troubleshooting

### "Not logged in" status
- Make sure you're logged into your Twenty instance
- Try refreshing the Twenty page
- Check that the Twenty URL in settings matches exactly

### "Connection failed"
- Verify your Twenty URL is correct
- Ensure Twenty is accessible from your browser
- Check browser console for errors

### Profile data not captured correctly
- LinkedIn frequently changes their DOM structure
- Try refreshing the page
- Check the browser console for scraping errors

## License

MIT
