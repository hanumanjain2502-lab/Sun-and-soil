# SUN & SOIL — DATA ENTRY GUIDE

The workbook you supplied is already the correct database architecture for the website.

The website does not hard-code the safari catalogue. It reads the published content from Google Sheets.

## Recommended entry order

1. Config
2. Destinations
3. Seasons
4. Experiences
5. Routes
6. Recommendation_Rules
7. Images
8. Packages
9. Email_Templates

## Destinations

Every destination should have a unique Destination_ID.

Example structure:
Destination_ID | Country | Destination_Name | Region | Short_Description | Best_For | Suggested_Days | Season_Tags | Pair_With | Map_Lat | Map_Lng | Image_URL | Active

Use semicolons inside multi-value fields.

Example:
Migration; Big Five; Wildlife; Photography

## Map coordinates

Map_Lat and Map_Lng power the interactive Leaflet map.

Without coordinates the destination can still appear as a card, but it cannot become a map marker.

## Images

Put real image URLs into Image_URL.

Recommended:
- landscape destination hero: 16:9
- cards: 4:3 or 3:2
- mobile sections: 4:5 or 3:4

The site does not require images to be uploaded into the repository. It can load external image URLs from the sheet.

## Recommendation Rules

The recommendation engine is deterministic.

It reads:
- country
- month
- duration
- interests

and selects the first matching active rule by Priority.

This makes the recommendations controllable by Sun & Soil rather than unpredictable.

## Trip Requests

Do not manually add website leads here.

The write gateway appends them automatically.

Keep the existing headers unchanged.

## Analytics Events

The website can record:
- page_view
- planner_step
- destination_selected
- experience_selected
- lead submission

The write gateway appends these events.

## Important

The current workbook contains only a small number of example content rows.

The site is designed to scale as you add:
- Kenya destinations
- Tanzania destinations
- seasonal records
- experiences
- route legs
- recommendation rules
- images
- packages
