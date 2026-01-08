# 📝 LinkedIn Content Automation

> **Transform YouTube videos into engaging LinkedIn posts automatically**

## The Problem

Creating consistent LinkedIn content is time-consuming:
- Watching videos and extracting key insights
- Summarizing content in an engaging format
- Formatting for LinkedIn's audience
- Manual posting takes 45+ minutes per post

**Result:** Inconsistent posting, missed opportunities for visibility.

## The Solution

End-to-end automated pipeline that:
- 🎬 **Tracks** YouTube videos you watch (via webhook or browser extension)
- 📝 **Extracts** transcripts automatically
- 🧠 **Analyzes** content relevance for your LinkedIn audience
- ✍️ **Generates** engaging posts with AI
- 📤 **Posts** directly to LinkedIn (with WhatsApp approval)

## Impact

| Metric | Value |
|--------|-------|
| ⏱️ **Time Saved** | 45 mins per post |
| 📈 **Output** | 1 post/day capability |
| ✅ **Setup Time** | 20 minutes |
| 🎯 **Consistency** | Never miss a post |

## Tech Stack

| Component | Technology |
|-----------|------------|
| **Orchestration** | n8n |
| **Transcript** | YouTube Transcript API + Supadata fallback |
| **Primary AI** | Google Gemini 2.5 Flash |
| **Fallback AI** | Groq (Llama 4 Maverick) + OpenRouter |
| **Storage** | Google Sheets (tracking + posts) |
| **Approval** | WhatsApp Business API |
| **Publishing** | LinkedIn API |

## How It Works

### Pipeline 1: Video Tracking & Relevance Check
```
YouTube Watch → Webhook → Extract Transcript → Truncate → AI Relevance Check
                                                              ↓
                                              Relevant? → Add to Queue
                                                 ↓ No
                                              Mark as Skipped
```

### Pipeline 2: Content Generation & Posting
```
New Relevant Video → Get Transcript → AI Summary → Generate Post → WhatsApp Approval → LinkedIn
                          ↓
                   Long transcript?
                          ↓ Yes
                   Chunk + Summarize Each → Aggregate
```

### AI Features:
- **Relevance Scoring**: Filters videos for AI/ML/Tech/Productivity topics
- **Comprehensive Analysis**: Extracts key concepts, takeaways, practical applications
- **Engaging Hooks**: Creates attention-grabbing first lines
- **Casual Tone**: Storytelling style with emojis and humor

## Workflow Components

| Stage | Nodes Used |
|-------|------------|
| **Trigger** | Google Sheets Trigger / Webhook |
| **Transcript** | HTTP Request to Transcript APIs |
| **Processing** | Code nodes for chunking long transcripts |
| **AI Analysis** | Gemini + Groq agents with fallbacks |
| **Storage** | Google Sheets (3 sheets: tracker, relevant, posts) |
| **Approval** | WhatsApp Send & Wait |
| **Publishing** | LinkedIn node |

## Quick Start

1. **Import** `workflow.json` into n8n
2. **Configure credentials:**
   - YouTube Transcript API key
   - Google Gemini API
   - Groq API
   - Google Sheets OAuth2
   - WhatsApp Business API
   - LinkedIn OAuth2
3. **Create Google Sheets:**
   - `youtube videos tracker` - all watched videos
   - `relevant videos` - filtered for your niche
   - Main sheet - generated posts
4. **Set up trigger:**
   - Browser extension webhook OR
   - Google Sheets trigger for manual adds
5. **Activate** the workflow

## Configuration Required

| Credential | Purpose |
|------------|---------|
| `Google Sheets OAuth2` | Track videos & store posts |
| `Google Gemini API` | Primary AI processing |
| `Groq API` | Fallback AI + chunk processing |
| `OpenRouter API` | Secondary fallback |
| `WhatsApp Business API` | Approval notifications |
| `LinkedIn OAuth2` | Auto-posting |

## Sample Output

**Input:** 10-minute tech YouTube video on AI tools

**Generated LinkedIn Post:**
```
🚀 Just watched a killer breakdown on AI agent frameworks...

Here's what blew my mind:

1. Most people are using AI wrong - they're prompting, not orchestrating
2. The real power is in chaining models together
3. Error handling in AI workflows is an art form

Spent 10 minutes learning, saved myself 10 hours of trial and error.

The future isn't about knowing AI. It's about knowing how to make AI work FOR you.

What's the last AI tool that actually changed how you work?

#AI #Automation #n8n #ProductivityHacks
```

---

[← Back to Portfolio](../../PORTFOLIO.md)
