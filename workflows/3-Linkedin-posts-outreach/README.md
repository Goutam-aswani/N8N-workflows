# 💼 LinkedIn Job Post Outreach Automation

> **Discover hidden job opportunities by scraping LinkedIn posts and auto-generating personalized outreach messages**

## The Problem

Traditional job hunting on LinkedIn has major limitations:
- LinkedIn's job board is oversaturated with outdated listings
- Many companies announce hiring through **posts first** before formal job postings
- Hiring managers often share opportunities in their personal posts
- Manually tracking and responding to these posts takes **hours daily**
- Generic applications get ignored - personalized outreach is critical

**Result:** You miss hidden opportunities and waste time on inefficient job searches.

## The Solution

Intelligent automation that finds job posts and generates personalized outreach:
- 🔍 **Scrapes** LinkedIn posts based on your search terms (e.g., "hiring", "job opening")
- 🧠 **AI Classification** filters posts to identify actual hiring opportunities
- ✍️ **Generates** personalized outreach messages using AI
- 📧 **Extracts** contact information (emails, profiles) automatically
- 📱 **WhatsApp notifications** for manual review before sending
- 📊 **Tracks** all posts and processed status in Google Sheets
- ⏰ **Runs automatically** every 6 hours to catch fresh posts

## Impact

| Metric | Value |
|--------|-------|
| ⏱️ **Time Saved** | 3-4 hours/day = **90+ hours/month** |
| 🎯 **Accuracy** | AI filters 85% of irrelevant posts |
| ✅ **Setup Time** | 25 minutes |
| 📈 **Output** | 10-15 qualified leads/day |
| 🚀 **Response Time** | Within 6 hours of post |

## Tech Stack

| Component | Technology |
|-----------|------------|
| **Orchestration** | n8n |
| **Primary AI** | Groq (Llama 3.3 70B) |
| **Fallback AI** | OpenRouter (DeepSeek R1, Llama 3.3) |
| **Storage** | Google Sheets (tracking + posts) |
| **Scraping** | Browser automation / LinkedIn scraper |
| **Notification** | WhatsApp Business API |
| **Trigger** | Schedule (every 6 hours) + Google Sheets Trigger |

## How It Works

### Pipeline 1: Post Discovery & Classification
```
Schedule Trigger (6h) → Get LinkedIn Posts → Loop Through Posts
                              ↓
                     Check if Already Processed?
                              ↓ No
                     AI Classification (HIRING vs NOT HIRING)
                              ↓ HIRING
                     Extract Contact Info → Save to Sheet
```

### Pipeline 2: Personalized Outreach Generation
```
Google Sheets Trigger → Get Post Details → AI Outreach Generator
                              ↓
                     Parse Message (JSON) → WhatsApp Notification
                              ↓
                     Manual Approval → Update Sheet (processed)
```

### AI Features:
- **Hiring Classification**: 
  - Identifies explicit job openings
  - Filters out personal achievements, thought leadership, service offerings
  - Extracts key indicators: "we're hiring", "join our team", job requirements
  
- **Personalized Message Generation**:
  - Extracts job title and requirements from post
  - Matches your skills to their needs
  - Creates short, punchy messages (150 words max)
  - Includes portfolio link naturally
  - Professional but conversational tone

## Workflow Components

### Trigger Nodes:
- **Schedule Trigger**: Runs every 6 hours to scrape fresh posts
- **Google Sheets Trigger**: Monitors sheet for new relevant posts

### Processing Nodes:
| Stage | Nodes Used |
|-------|------------|
| **Data Retrieval** | Google Sheets Get Row(s) |
| **Loop Processing** | Split in Batches (batch processing) |
| **AI Classification** | AI Agent (Groq/OpenRouter) - Hiring filter |
| **Contact Extraction** | Edit Fields (parse emails, profiles) |
| **Outreach Generation** | AI Agent (personalized message) |
| **Approval** | WhatsApp Send Message |
| **Tracking** | Google Sheets Update Row |

### Conditional Logic:
- **If Node 1**: Checks if post has valid LinkedIn profile + not processed
- **If Node 2**: Validates email extraction (contains "@")

### AI Agents:
1. **Hiring Classifier Agent**:
   - System prompt: Precise hiring content detection
   - Output: JSON with classification, confidence, reasoning
   - Filters: Generic posts, certifications, service offerings

2. **Outreach Generator Agent**:
   - System prompt: Expert recruiter outreach specialist
   - Output: JSON with subject, message, tone
   - Personalization: References specific job details, matches skills

## Quick Start

### 1. Import Workflow
```bash
# Import workflow.json into your n8n instance
```

### 2. Configure Credentials
| Credential | Purpose |
|------------|---------|
| `Google Sheets OAuth2` | Read/write posts and tracking data |
| `Groq API` | Primary AI model (Llama 3.3) |
| `OpenRouter API` | Fallback AI models |
| `WhatsApp Business API` | Approval notifications |

### 3. Set Up Google Sheets
Create a sheet with these columns:
| Column | Description |
|--------|-------------|
| `Poster Name` | Name of person posting |
| `Poster Profile` | LinkedIn profile URL |
| `Post Content` | Full post text |
| `emails` | Extracted email addresses |
| `processed` | Status: "yes" / "no" |
| `timestamp` | When post was scraped |

### 4. Configure LinkedIn Scraping
You can use:
- **Browser automation** (Selenium/Puppeteer)
- **LinkedIn scraper service** (Apify, PhantomBuster)
- **Manual CSV upload** (for testing)

Add scraped posts to the Google Sheet with `processed = "no"`

### 5. Customize AI Prompts
Edit the AI Agent system messages to:
- Update your background/skills
- Change portfolio link
- Adjust tone (more casual/formal)
- Modify search keywords

### 6. Set Schedule
- Default: Every 6 hours
- Adjust based on your job search intensity
- Consider API rate limits

### 7. Activate Workflow
1. Test with sample post first
2. Verify WhatsApp notifications work
3. Check message quality
4. Enable schedule trigger

## Configuration Details

### AI Classification Criteria

**HIRING Posts Include:**
- Explicit job openings or recruitment announcements
- "We're hiring", "looking for", "join our team"
- Job requirements and qualifications
- Application instructions or contact info

**NOT HIRING Posts:**
- Personal achievements (certifications, completions)
- Thought leadership or industry insights
- Service offerings or consulting
- Automation showcases without recruitment

### Outreach Message Formula
```
[Attention Hook] - Reference their specific role
[Value Prop] - Match 2-3 of your skills to their needs
[Social Proof] - Portfolio link naturally mentioned
[Call to Action] - Clear next step (coffee chat, resume, etc.)
```

### Sample Input/Output

**Input Post:**
```
🚀 We're hiring a Python Automation Engineer!

Looking for someone with:
- Strong Python skills
- API integration experience
- n8n or workflow automation background

DM me if interested!
```

**AI Generated Output:**
```json
{
  "subject": "Quick message about Python Automation Engineer role",
  "message": "Hi [Name], saw your post about the Python Automation Engineer position. I've built 5 production n8n workflows handling API integrations and data pipelines (check out my portfolio: https://goutam-aswani.github.io/N8N-workflows/). Would love to chat about how my automation experience fits what you're looking for. Open for a quick call this week?",
  "tone": "professional"
}
```

**WhatsApp Notification:**
```
poster profile: linkedin.com/in/hiring-manager

message to send: Quick message about Python Automation Engineer role
Hi [Name], saw your post about the Python Automation Engineer position...
```

## Customization Options

### Search Terms
Modify scraping keywords:
- "hiring"
- "we're looking for"
- "job opening"
- "join our team"
- "[Your specialty] position"

### AI Models
Primary: **Groq Llama 3.3 70B** (fast, accurate)
Fallbacks: 
- DeepSeek R1 (reasoning)
- OpenRouter Llama 3.3 (reliability)

### Batching
- Current: Processes posts sequentially
- Adjust `Split in Batches` for parallel processing
- Be mindful of API rate limits

### Approval Flow
- **Current**: WhatsApp notification for manual review
- **Alternative**: Auto-send with confidence threshold
- **Option**: Email approval instead of WhatsApp

## Troubleshooting

### Issue: Too many false positives
**Solution:** Adjust AI classification prompt to be more strict

### Issue: Messages too generic
**Solution:** Add more context about your background in the prompt

### Issue: Rate limit errors
**Solution:** Increase delay between batches, reduce frequency

### Issue: No posts found
**Solution:** Verify scraper is working, check search terms

## Best Practices

1. **Test thoroughly** before going live
2. **Review AI messages** for first few days
3. **Update your skills** in prompt regularly
4. **Track response rates** to optimize messaging
5. **Respect LinkedIn limits** - don't spam
6. **Personalize further** after AI generation
7. **Follow up** on conversations promptly

## Future Enhancements

- [ ] Add sentiment analysis for post relevance
- [ ] Track application outcomes
- [ ] A/B test different message templates
- [ ] Auto-respond to replies via LinkedIn API
- [ ] Company research integration (Crunchbase/LinkedIn)
- [ ] Skill matching score (you vs. requirements)

---

## Privacy & Ethics Note

⚠️ **Important:**
- Only scrape public LinkedIn posts
- Respect LinkedIn's Terms of Service
- Don't spam or send unsolicited messages excessively
- Always provide opt-out options
- Use this tool responsibly for genuine job search

---

[← Back to Portfolio](../../PORTFOLIO.md)
