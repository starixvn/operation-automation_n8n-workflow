# Search New Team Workflow - Diagrams

This document illustrates the n8n workflow for searching and verifying team names with AI-powered translation.

## Workflow Overview

### Stage 1: Data Retrieval
- Manual trigger initiates the workflow
- Fetches team names from Google Sheets (Input sheet)
- Filters to extract only the "Team Name" field

### Stage 2: Team Verification
- Uses OpenAI to verify if the team name is correct
- Searches authoritative sources (Wikipedia, UEFA, ESPN, official websites)
- Returns structured JSON with TeamName, Result (Correct/Incorrect), and WebSite URLs

### Stage 3: Conditional Processing
**If Team is Correct:**
1. Translates team name to multiple languages (Traditional Chinese, Simplified Chinese, Vietnamese, Thai, English)
2. Verifies all translations against authoritative sources
3. If all translations are correct → appends full data to Output sheet
4. If translations are incorrect → appends partial data to Output sheet

**If Team is Incorrect:**
- Appends verification data only (no translations) to Output sheet

### Stage 4: Loop Processing
- Processes items in batches (batch size = 1)
- Continues until all team names are processed

## Output Fields
- TeamName
- Result (Correct/Incorrect)
- WebSite (comma-separated URLs)
- Traditional Chinese
- Simplified Chinese
- Vietnamese
- Thai
- English
