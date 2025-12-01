# Quick Start Checklist

A condensed checklist for setting up the AI Triathlon Coach workflow. See [README.md](README.md) for detailed instructions.

## Pre-Setup: Gather Required Information

- [ ] OpenAI API key ([Get it here](https://platform.openai.com/api-keys))
- [ ] Strava account credentials
- [ ] Your Telegram bot token and chat ID
- [ ] Your race details (name, date, type)
- [ ] Your metrics (weight, resting HR, max HR)

## Step 1: Create Data Tables (5 min)

- [ ] Create **Training** table with 10 columns (see DATA_TABLES.md)
- [ ] Create **Training Plan** table with 4 columns (see DATA_TABLES.md)
- [ ] Save both Data Table IDs

## Step 2: Set Up External Services (10 min)

- [ ] Create Strava API application → Save Client ID & Secret
- [ ] Create Telegram bot via @BotFather → Save Bot Token
- [ ] Get your Telegram Chat ID → Save Chat ID
- [ ] Get OpenAI API key → Save API Key

## Step 3: Create n8n Credentials (5 min)

- [ ] Add Strava OAuth2 credential
- [ ] Add Telegram API credential
- [ ] Add OpenAI API credential
- [ ] Add Google Calendar OAuth2 credential (optional)

## Step 4: Import & Configure Workflow (10 min)

- [ ] Import `Coach_Template.json` into n8n
- [ ] Assign credentials to all nodes:
  - [ ] Get Latest Strava Activity → Strava
  - [ ] OpenAI Chat Model (3 nodes) → OpenAI
  - [ ] Telegram nodes (2 nodes) → Telegram
  - [ ] Create Calendar Events → Google Calendar
- [ ] Update both Telegram nodes with your Chat ID
- [ ] Update all 6 data table node references with your Table IDs

## Step 5: Personalize Configuration (5 min)

- [ ] Edit **Workflow Configuration** node:
  - [ ] Set `raceDate` to your race date
  - [ ] Set `raceName` to your race name
  - [ ] Set `raceType` to your race type
- [ ] Edit **Convert KM to Miles** code node:
  - [ ] Update `USER_WEIGHT_LBS`
  - [ ] Update `USER_RESTING_HR`
  - [ ] Update `USER_MAX_HR`

## Step 6: Test (5 min)

- [ ] Test activity monitoring: Execute "Every 5 Minutes" node
  - [ ] Verify activity appears in Training table
  - [ ] Verify Telegram message received
- [ ] Test training plan: Execute "Every Sunday" node
  - [ ] Verify plan appears in Training Plan table
  - [ ] Verify calendar events created
  - [ ] Verify Telegram summary received

## Step 7: Activate

- [ ] Toggle workflow to **Active**
- [ ] Done! Workflow will now run automatically

## Estimated Total Time: 40 minutes

## Troubleshooting

**No Strava data?** → Check Strava API credentials
**No Telegram messages?** → Verify bot token and chat ID
**AI not working?** → Check OpenAI API key and credits
**Data table errors?** → Verify table IDs are correct

See [README.md](README.md) for detailed troubleshooting.

## Support

- [n8n Documentation](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
- Review DATA_TABLES.md for schema details
- Review README.md for complete setup guide
