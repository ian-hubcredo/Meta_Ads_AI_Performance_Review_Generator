# Meta Ads Performance Analysis to AI-Generated Ad Concepts

## Overview

This workflow automates the entire Meta (Facebook) ads performance review cycle. Every weekday, it pulls ad performance data from the Meta Graph API, scores each ad based on CTR, CPC, and conversions, routes them into High/Medium/Low performance tiers, extracts winning patterns from top performers, and uses Claude AI to generate 5 new ad concepts based on what is working. The results are written to a Google Doc from a template and logged in a Notion database for team review. Errors trigger a Slack/Teams notification automatically.

## How It Works

```
Schedule (weekday 9am) -> Configure API keys -> Get Meta Ads -> Get Ad Insights (last 7 days) -> Score and tier each ad -> Route by performance (High/Medium/Low) -> Extract winning patterns from High -> Build AI prompt -> Claude generates 5 new ad concepts -> Copy Google Doc template -> Insert analysis + concepts -> Create Notion page with metrics + doc link
```

### Workflow Diagram

```mermaid
flowchart TD
    A["Schedule Trigger\nWeekday 9am"] --> B["Set\nWorkflow Config"]
    B --> C["Meta API\nGet All Ads"]
    C --> D["Meta API\nGet 7-Day Insights"]
    D --> E["Code\nScore and Tier Ads"]
    E --> F{"Route by\nPerformance"}
    F -- High --> G["Extract\nWinning Patterns"]
    F -- Medium --> H["Google Sheets\nLog Medium"]
    F -- Low --> I["Google Sheets\nLog Low"]
    G --> J["Build\nAI Prompt"]
    J --> K["Claude AI\nGenerate 5 Ad Concepts"]
    K --> L["Google Docs\nCopy Template"]
    L --> M["Google Docs\nInsert Analysis"]
    M --> N["Notion\nCreate Review Page"]

    style A fill:#1B3A4B,color:#fff
    style C fill:#2C5F7C,color:#fff
    style E fill:#3D5A80,color:#fff
    style K fill:#4A6D7C,color:#fff
    style N fill:#274C36,color:#fff
```

## Integrations

- **Meta Graph API** - Ad and insights data retrieval
- **Anthropic Claude (3.5 Sonnet)** - AI-generated ad concepts based on winning patterns
- **Google Docs** - Templated performance report generation
- **Google Sheets** - Medium and low performer logging
- **Notion** - Review tracking database with metrics and doc links
- **Slack/Teams** - Error notifications via webhook

## Setup

1. Import `Meta_Ads_Performance_Analysis_to_AI_Generated_Ad_Concepts.json` into your n8n instance.
2. Update the Workflow Configuration node with your Meta Ad Account ID, Meta Access Token, Claude API Key, Google Doc Template ID, and Notion Database ID.
3. Configure Google OAuth2 credentials for Docs and Sheets.
4. Configure Notion credentials.
5. Set the error notification webhook URL (Slack or Teams).
6. Customize the performance scoring thresholds if needed.
7. Activate the workflow.
