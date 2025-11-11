# Operation Automation – n8n Workflows

This repository stores **n8n workflows** for the Operation Automation project.
It is jointly maintained by the **Taiwan RAID/DS team** and the **Vietnam Nexcel team**.

## 📋 Project Scope

### Core Automation Tasks
- **Create Event** - Automated event creation workflows
- **Event Check** - Event validation and monitoring
- **Get Result** - Result extraction and processing
- **Trader Assignment** - Automated trader task distribution
- **IPTV Data Processing** - Daily IPTV and Infosite data extraction and merging

### Additional Automation
- Data synchronization between systems
- Report generation and distribution
- Scheduled task execution
- Email notifications and alerts

## 🏗️ Current Workflows

### IPTV Workflows (`IPTV/`)
**Purpose**: Automated daily extraction and processing of IPTV and Infosite data

#### IPTV_MAIN_Schedule
- **Schedule**: Weekly on Sunday, Wednesday, Thursday, Friday, Saturday at 7:00 AM
- **Function**: Main scheduler that triggers IPTV_schedule workflow

**Process Flow**:
1. **Date Calculation** - Generates today and tomorrow dates in multiple formats (YYYY-MM-DD, DD/MM/YYYY)
2. **IPTV Data Extraction** - Downloads IPTV data via HTTP API call
3. **League Processing** - Retrieves and processes league information for multiple sources:
   - Soccerway
   - IMG
   - Virtual
   - RB Upload
   - RTS Upload
   - BG Upload
   - BETRADAR Upload
4. **Infosite Data Extraction** - Downloads infosite data with batch processing (50 items per batch)
5. **Wait Period** - Dynamic wait time based on batch count
6. **Data Merging** - Combines IPTV and Infosite data into Excel format
7. **File Download** - Retrieves the merged Excel file
8. **Email Distribution** - Sends results to stakeholders

#### IPTV_insert_DB
- **Purpose**: Inserts IPTV event data into database
- **Process Flow**:
  1. **Date Calculation** - Generates today and tomorrow dates (UTC+8)
  2. **Data Splitting** - Splits events into batches of 20 items
  3. **Database Insertion** - Posts events to Event Collecting Service API
  4. **Batch Processing** - Processes events in batches using loop

#### IPTV_current
- **Purpose**: Current IPTV data processing workflow

**API Endpoints**:
- `http://10.18.200.198:8000/download-iptv` - IPTV data extraction
- `http://10.18.200.198:8000/check-leagues` - League information
- `http://10.18.200.198:8000/download-infosite` - Infosite data extraction
- `http://10.18.200.198:8000/merge-to-excel` - Data merging
- `http://10.18.200.198:8000/download-excel` - File download
- `https://eventcollectingservice.kl.starixuat.com/IPTV/events` - Event database insertion

### BetCity Workflow (`BetCity/`)
- **BetCity - Event.json**: BetCity event processing workflow

### BWF Workflow (`BWF/`)
- **BWF_Crawler.json**: BWF (Badminton World Federation) data crawler workflow

### Futbol24 Workflow (`Futbol24/`)
- **Futbol24 - Event.json**: Futbol24 event processing workflow

### SearchAndCheckWithOpenAI Workflow (`SearchAndCheckWithOpenAI/`)
- **search_new_team.json**: AI-powered team name validation and translation workflow
- **Purpose**: Validates soccer team names using AI and translates them into multiple languages
- **Features**:
  - Team name validation using OpenAI
  - Multi-language translation (Traditional Chinese, Simplified Chinese, Vietnamese, Thai, English)
  - Google Sheets integration for input/output
  - Batch processing with error handling
- **See**: `SearchAndCheckWithOpenAI/README.md` for detailed documentation


## 🛠️ Technical Requirements

### n8n Setup
- n8n version compatible with node types used
- SMTP credentials configured for email sending
- HTTP request capabilities enabled
- Schedule trigger functionality

### Dependencies
- Access to internal API endpoints (10.18.200.198:8000)
- SMTP server configuration (VN_SMTP credentials)
- Appropriate network access for API calls

### Node Types Used
- `n8n-nodes-base.httpRequest` - API communications
- `n8n-nodes-base.code` - Custom JavaScript processing
- `n8n-nodes-base.emailSend` - Email notifications
- `n8n-nodes-base.wait` - Workflow pausing
- `n8n-nodes-base.scheduleTrigger` - Automated execution
- `n8n-nodes-base.stickyNote` - Documentation

## 📁 Repository Structure

```
n8n-workflow/
├── README.md                          # This documentation
├── IPTV/                              # IPTV data processing workflows
│   ├── IPTV_MAIN_Schedule.json        # Main scheduler workflow
│   ├── IPTV_schedule.json             # Scheduled IPTV data processing
│   ├── IPTV_insert_DB.json            # Database insertion workflow
│   └── IPTV_current.json              # Current IPTV processing
├── BetCity/                           # BetCity workflows
│   └── BetCity - Event.json           # BetCity event processing
├── BWF/                               # BWF workflows
│   └── BWF_Crawler.json               # BWF data crawler
├── Futbol24/                          # Futbol24 workflows
│   └── Futbol24 - Event.json          # Futbol24 event processing
└── SearchAndCheckWithOpenAI/          # AI-powered team validation
    ├── README.md                      # Detailed workflow documentation
    ├── search_new_team.json           # Team name validation workflow
    ├── n8n_example.png                # Workflow diagram
    └── workflow-sequence-diagram.md   # Sequence diagram documentation
```

## 🚀 Getting Started

### Import Workflow
1. Open your n8n instance
2. Go to **Workflows** → **Import from File**
3. Select the desired `.json` file from this repository
4. Configure credentials and endpoints as needed
5. Test the workflow before activating

### Configuration Checklist
- [ ] SMTP credentials configured (`VN_SMTP`)
- [ ] API endpoints accessible
- [ ] Email recipients updated if needed
- [ ] Schedule trigger configured correctly
- [ ] Test run completed successfully

## 📝 Contribution Guide

### Adding New Workflows
1. **Export** workflow from n8n in **JSON format**
2. **Name** the file descriptively (e.g., `EventCheck.json`)
3. **Organize** workflows into appropriate directories:
   - Create a new directory if it's a new workflow category
   - Place related workflows in the same directory
   - Use descriptive directory names (e.g., `IPTV/`, `BetCity/`)
4. **Update** this README.md with workflow details
5. **Add** a detailed README.md in the workflow directory if the workflow is complex
6. **Test** the workflow thoroughly
7. **Open** a Merge Request for review

### Workflow Documentation Template
When adding new workflows, include:
- **Purpose** - What the workflow accomplishes
- **Schedule** - When it runs (if automated)
- **Process Flow** - Step-by-step description
- **Dependencies** - Required credentials/endpoints
- **Recipients/Outputs** - Where results go

### Best Practices
- Use descriptive node names
- Add sticky notes for documentation
- Include error handling where appropriate
- Test with sample data before deployment
- Document any custom code or complex logic

## 🔧 Maintenance

### Regular Tasks
- Monitor workflow execution logs
- Update API endpoints if they change
- Review and update email recipient lists
- Test workflows after n8n updates
- Backup workflow configurations

### Troubleshooting
- Check API endpoint availability
- Verify credentials are not expired
- Review workflow execution history
- Check email delivery status
- Validate data formats and structures

---

