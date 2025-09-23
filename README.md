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

### IPTV Workflow (`IPTV.json`)
**Purpose**: Automated daily extraction and processing of IPTV and Infosite data

**Schedule**: Daily at 17:01 (5:01 PM)

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

**Recipients**:
- robert.tseng@onelab.tw
- ben.chen@onelab.tw
- lientruong0508@gmail.com
- sukyfeng87@gmail.com
- rdrd33@gmail.com

**API Endpoints**:
- `http://10.18.200.198:8000/download-iptv` - IPTV data extraction
- `http://10.18.200.198:8000/check-leagues` - League information
- `http://10.18.200.198:8000/download-infosite` - Infosite data extraction
- `http://10.18.200.198:8000/merge-to-excel` - Data merging
- `http://10.18.200.198:8000/download-excel` - File download

## 👥 Team Responsibilities

### Taiwan Team (RAID/DS)
- Develop workflows for major leagues/events
- Initial workflow development and architecture
- Core system integration
- Performance optimization

### Vietnam Team (Nexcel)
- Maintain workflows for additional leagues/sports
- Extend integration capabilities
- Contribute enhancements and improvements
- Monitor and troubleshoot existing workflows

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
├── README.md          # This documentation
├── IPTV.json          # IPTV data processing workflow
└── [future workflows] # Additional workflows will be added here
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
3. **Place** the JSON file in the repository root
4. **Update** this README.md with workflow details
5. **Test** the workflow thoroughly
6. **Open** a Merge Request for review

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

## 📞 Support

For issues or questions:
- **Taiwan Team**: Contact RAID/DS team members
- **Vietnam Team**: Contact Nexcel team members
- **Technical Issues**: Check n8n logs and API responses
- **Repository Issues**: Create an issue or merge request

---

**Last Updated**: September 2025
**Maintained By**: Taiwan RAID/DS Team & Vietnam Nexcel Team

