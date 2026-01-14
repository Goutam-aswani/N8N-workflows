# 🔄 n8n Workflows Portfolio

[![GitHub Pages](https://img.shields.io/badge/Live%20Demo-Visit%20Site-blue?style=for-the-badge&logo=github)](https://goutam-aswani.github.io/N8N-workflows/)
[![n8n](https://img.shields.io/badge/Built%20with-n8n-orange?style=for-the-badge&logo=n8n)](https://n8n.io)

> **Production-ready workflow automations** that save time, eliminate errors, and scale effortlessly.

---

## 👋 About

This repository showcases my n8n automation projects — real solutions to real problems. Each workflow is documented with:
- 📝 Detailed README explaining the problem & solution
- 📊 Impact metrics (time saved, accuracy, setup time)
- 🔧 Tech stack and configuration guide
- 📦 Ready-to-import `workflow.json`

---

## 🚀 Featured Workflows

### 1. [SMS Expense Tracker](./workflows/1-sms-expense-tracker/)

**Automatically log bank transactions from SMS → Google Sheets**

| Impact | Value |
|--------|-------|
| ⏱️ Time Saved | 30 hours/year |
| 💰 Accuracy | 98% |
| ✅ Setup | 15 minutes |

**How it works:**
- 📩 Webhook receives SMS from bank notifications
- 🧠 Gemini AI parses transaction details (with Groq fallback)
- 🔄 Auto-categorizes as CREDIT or DEBIT
- 📊 Logs to Google Sheets in real-time

**Tech:** `n8n` `Gemini 2.5 Flash` `Groq` `Google Sheets` `Webhook`

---

### 2. [LinkedIn Content Automation](./workflows/2-linkedin-automation/)

**Transform YouTube videos into engaging LinkedIn posts automatically**

| Impact | Value |
|--------|-------|
| ⏱️ Time Saved | 45 min/post |
| 📈 Output | 1 post/day |
| ✅ Setup | 20 minutes |

**How it works:**
- 🎬 Tracks YouTube videos you watch
- 📝 Extracts transcripts automatically
- 🎯 AI filters for relevance to your niche
- ✍️ Generates engaging LinkedIn posts
- 📱 WhatsApp approval before auto-posting

**Tech:** `n8n` `YouTube API` `Gemini AI` `Groq` `WhatsApp` `LinkedIn API`

---

### 3. [LinkedIn Job Post Outreach](./workflows/3-Linkedin-posts-outreach/)

**Discover hidden job opportunities by scraping LinkedIn posts and auto-generating personalized outreach**

| Impact | Value |
|--------|-------|
| ⏱️ Time Saved | 90+ hours/month |
| 🎯 Accuracy | 85% AI filtering |
| ✅ Setup | 25 minutes |

**How it works:**
- 🔍 Scrapes LinkedIn posts for job-related content every 6 hours
- 🧠 AI classification filters actual hiring posts from noise
- ✍️ Generates personalized outreach messages with AI
- 📧 Extracts contact information automatically
- 📱 WhatsApp approval before sending
- 📊 Tracks all posts and status in Google Sheets

**Tech:** `n8n` `Groq (Llama 3.3)` `OpenRouter` `Google Sheets` `WhatsApp`

---

## 📊 Portfolio Stats

| Metric | Value |
|--------|-------|
| 🤖 Workflows | 3 |
| ⏱️ Time Saved | 165+ hours/year |
| 🔌 APIs Integrated | 10+ |
| 🧠 AI Models | Gemini, Groq, Llama, DeepSeek |

---

## 🛠️ How to Use

1. **Browse** the [workflows](./workflows/) folder
2. **Read** the README for setup instructions
3. **Import** `workflow.json` into your n8n instance
4. **Configure** credentials as documented
5. **Activate** and start automating!

---

## 🌐 Live Demo

Visit the **[Landing Page](https://goutam-aswani.github.io/N8N-workflows/)** for a visual overview.

---

## 📫 Connect

- **GitHub**: [github.com/Goutam-Aswani](https://github.com/Goutam-Aswani)
- **LinkedIn**: [linkedin.com/in/goutam-aswani-bei143](https://www.linkedin.com/in/goutam-aswani-bei143/)
- **Email**: goutamaswani43@gmail.com

---

<p align="center">
  <sub>Built with ❤️ using n8n</sub>
</p>
