# SUN & SOIL — AFRICA SAFARI PLANNER (STATIC EDITION)

This version removes the website UI from Google Apps Script.

The public website is normal HTML/CSS/JavaScript and can be hosted on:
- GitHub Pages
- Netlify
- Vercel
- any normal static web host

Google Sheets remains the content database and lead database.

## Architecture

PUBLIC WEBSITE
    ↓
HTML / CSS / JavaScript
    ↓
Google Sheets (published read-only data)
    +
Google Apps Script Web App (write-only gateway)
    ↓
Trip_Requests / Analytics_Events

The website itself is NOT served by Apps Script.

## Files

- index.html — cinematic home
- explore.html — destination explorer
- planner.html — interactive safari builder + Leaflet map
- contact.html — direct enquiry
- success.html — personalised submission confirmation
- assets/css/styles.css — complete design system
- assets/js/config.js — THE ONLY WEBSITE CONFIG FILE
- assets/js/data.js — Google Sheets reader
- assets/js/app.js — shared UI / analytics
- assets/js/planner.js — planner engine
- google-apps-script/Code.gs — Google Sheet write gateway

## STEP 1 — Put the workbook in Google Sheets

Use your existing:
Sun & Soil — Africa Safari Planner

Keep the same tabs and headers.

The current workbook has:
Config
Destinations
Seasons
Experiences
Routes
Packages
Trip_Requests
Recommendation_Rules
Images
Analytics_Events
Email_Templates
README

Public rates are not displayed by the website.

## STEP 2 — Make the sheet readable by the public site

For the data-reading layer, publish the spreadsheet or otherwise make the relevant tabs publicly readable.

Google Sheets:
File → Share / Publish to web

The website reads the tabs through Google's gviz endpoint.

Do not put private customer data into the public-facing data tabs.

Trip_Requests and internal operational data should be treated as private.

## STEP 3 — Create the write gateway

Open the Google Sheet:

Extensions → Apps Script

Paste:

google-apps-script/Code.gs

This script only writes leads and analytics to the workbook.

Deploy:
Deploy → New deployment
Type: Web app
Execute as: Me
Who has access: Anyone

Copy the `/exec` URL.

## STEP 4 — Configure the website

Open:

assets/js/config.js

Change ONLY:

GOOGLE_SHEET_URL:
"YOUR GOOGLE SHEET URL"

WRITE_API_URL:
"YOUR APPS SCRIPT /exec URL"

Example:

GOOGLE_SHEET_URL: "https://docs.google.com/spreadsheets/d/XXXXXXXX/edit"

WRITE_API_URL: "https://script.google.com/macros/s/XXXXXXXX/exec"

You do not paste the spreadsheet link into every HTML page.
You paste it ONCE in config.js.

## STEP 5 — Host the website

For GitHub Pages:

1. Create a new repository.
2. Upload all files/folders while preserving structure.
3. Enable GitHub Pages from repository settings.
4. Open the generated site URL.
5. Use that URL for your QR code.

## IMPORTANT: CORS / WRITE BEHAVIOUR

The frontend intentionally sends lead data to Apps Script as a simple form-encoded POST with `no-cors`.

The user-facing page does not need to read the response. It displays the success page after the request is sent.

If the Apps Script deployment is not configured correctly, the lead will not be stored.

## DATA ENTRY

The Google Sheet is the content engine.

Populate:

### Destinations
One row per destination.
Required for map:
- Destination_ID
- Country
- Destination_Name
- Map_Lat
- Map_Lng
- Image_URL
- Active = TRUE

### Seasons
One row per seasonal period.
Use:
- Month_Start
- Month_End
- Season_Name
- Headline
- What_You_May_Experience
- Recommended_Areas
- Ideal_For
- Planner_Message

### Experiences
One row per experience.
Use:
- Experience_Name
- Country
- Suggested_Season
- Destination_IDs
- Image_URL

### Routes
One row per route leg.
Use:
- From_Destination_ID
- To_Destination_ID
- Days_Recommended
- Travel_Note

### Recommendation_Rules
This controls the deterministic Safari Assistant.
Example:
Tanzania + August + 5–10 days + Migration
→ Serengeti / Northern Serengeti

### Images
This is the scalable image library.
You can add 30–50 real destination/experience images here.
The website uses Image_URL first and a visual fallback only when the sheet is empty.

## SECURITY

Do not expose:
- Public_Rate
- internal supplier costs
- private lead notes
- operational credentials

The public website only reads the tabs it needs.

For a production launch, consider putting public content in a separate read-only Google Sheet and keeping Trip_Requests in a private operational workbook.

## CONTACT

India: +91 9637146111
Tanzania/Africa: +255 657 313 330
Email: info@sunandsoildestinations.com
Tagline: Crafting Soulful Journeys
