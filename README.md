# 📄 DocuSummarize Pro

> **Transform your documents into clear, actionable summaries and analysis with AI. Get key points, action items, and citations—instantly and accurate.** ⚡

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![Next.js](https://img.shields.io/badge/Next.js-15.1-black.svg)](https://nextjs.org/)
[![Railway](https://img.shields.io/badge/Deploy-Railway-blueviolet.svg)](https://railway.app/)

---

## ✨ Features

### 🎯 **Core Functionality**
- 📄 **Multi-Format Support** - PDF, Word, Excel, CSV, and Text files
- 🤖 **AI-Powered Summarization** - Get structured summaries with OpenAI
- 📊 **Excel/CSV Analysis** - Advanced data analysis with insights and recommendations
- ☁️ **Google Drive Integration** - Pick files directly from your Drive
- 💻 **Local File Upload** - Upload files from your computer
- 📝 **Custom Instructions** - Guide the AI with specific requirements

### 🎨 **Beautiful UI/UX**
- ✨ **Modern 2025 Design** - Glassmorphism, gradients, micro-animations
- 🌙 **Dark Mode** - Full theme support with smooth transitions
- 📱 **Fully Responsive** - Optimized for desktop, tablet, and mobile
- ♿ **Accessible** - WCAG AA compliant with keyboard navigation
- 🎯 **Intuitive Interface** - Clean, user-friendly design

### 📊 **Dashboard Features**
- 📈 **Usage Statistics** - Total documents, weekly summaries & analyses
- 📝 **Recent Activity** - Last 20 documents with previews
- 🔍 **Search & Filter** - Find documents by name, type, or date
- 👁️ **Full Result View** - Modal with complete markdown output
- 📋 **Copy to Clipboard** - One-click copy functionality

### 🚀 **Advanced Features**
- 🎯 **Structured Output** - Overview, Key Points, Action Items, Citations
- 📊 **Data Analysis** - For Excel/CSV: metrics, insights, recommendations
- 🔄 **Real-Time Processing** - Background job system with polling
- 💾 **Persistent History** - All results saved to database
- 🎚️ **Customizable** - Length (Brief/Standard/Detailed) & Tone (Neutral/Executive/Academic)

---

## 🏗️ Tech Stack

### **Backend** 🐍
- **FastAPI** - Modern Python web framework
- **OpenAI API** - GPT-4 for summarization & analysis
- **Python 3.11+** - Latest features and performance

### **Frontend** ⚛️
- **Next.js 15.1** - React 19 with App Router
- **Tailwind CSS** - Utility-first styling
- **shadcn/ui** - Beautiful component library
- **Lucide Icons** - Modern icon set

### **Database & Cache** 💾
- **Supabase** - PostgreSQL with real-time capabilities
- **Upstash Redis** - Serverless job queue & caching

### **External APIs** 🔌
- **Google Drive Picker** - File selection from Drive
- **Google OAuth 2.0** - Secure authentication

### **Deployment** 🚀
- **Railway** - Automated deployment platform
- **Vercel-ready** - Alternative deployment option

---

## 📸 Screenshots

### 🏠 Homepage
![Homepage](public/demo/homepage.png)
*Beautiful landing page with file type icons and clear value proposition*

### 🎮 Playground
![Playground](public/demo/playground.png)
*Interactive interface for summarization and analysis*

### 📊 Dashboard
![Dashboard](public/demo/dashboard.png)
*Comprehensive dashboard with stats, activity, and search*

---



## 📖 User Guide

### 🎮 Using the Playground

1. **Choose File Source**
   - 💻 **Local Computer** - Upload from your device
   - ☁️ **Google Drive** - Pick from Drive (requires OAuth)

2. **Select Files**
   - Click **"Browse Files"** or **"Pick from Drive"**
   - Supports: PDF, Word, Excel, CSV, Text

3. **Add Instructions (Optional)**
   - Guide the AI: *"Focus on financial metrics"*
   - Customize length & tone

4. **Process**
   - **Summarize** - For documents (PDFs, Word, Text)
   - **Analyze** - For data (Excel, CSV)

5. **View Results**
   - Overview, Key Points, Action Items
   - Copy markdown or download PDF

### 📊 Using the Dashboard

1. **View Stats**
   - Total documents processed
   - Summaries this week
   - Analyses this week

2. **Search & Filter**
   - Search by file name or content
   - Filter by type (Summary/Analysis)
   - Sort by date (Newest/Oldest)

3. **View Full Results**
   - Click any activity card
   - View complete markdown
   - Copy to clipboard

---

## 🎨 Customization

### Theme Options
- ☀️ **Light Mode** - Clean, bright interface
- 🌙 **Dark Mode** - Easy on the eyes
- 🖥️ **System** - Follows OS preference

### Density Options
- 🎯 **Comfort** - Spacious layout (default)
- 📦 **Compact** - Dense, efficient layout

### Summary Options
- **Length**: Brief, Standard, Detailed
- **Tone**: Neutral, Executive, Academic

---


---

## 👨‍💻 Creator

**Created by Derril Filemon**

---

## 🙏 Acknowledgments

- **OpenAI** - For GPT-4 API
- **Supabase** - For database & auth
- **Upstash** - For Redis caching
- **Railway** - For deployment
- **Vercel** - For Next.js
- **shadcn/ui** - For beautiful components

---

## 📞 Support

- 📧 **Email**: support@docusummarize.pro
- 🐛 **Issues**: [GitHub Issues](https://github.com/derril-tech/ai-document-summarizer-pro/issues)
- 💬 **Discussions**: [GitHub Discussions](https://github.com/derril-tech/ai-document-summarizer-pro/discussions)

---

<div align="center">

**⭐ Star this repo if you find it useful!**

Made with ❤️ and ☕ by [Derril Filemon](https://github.com/derril-tech)

</div>
