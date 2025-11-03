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

## 🚀 Quick Start

### Prerequisites
- **Python 3.11+**
- **Node.js 18+**
- **Supabase Account** (free tier works)
- **Upstash Redis** (free tier works)
- **OpenAI API Key**
- **Google Cloud Project** (for Drive Picker)

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/derril-tech/ai-document-summarizer-pro.git
cd ai-document-summarizer-pro
```

### 2️⃣ Environment Setup
Create `.env` in the root directory:

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=https://your-project.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-key
SUPABASE_SERVICE_ROLE=your-service-role-key
SUPABASE_SCHEMA=docusummarize

# OpenAI
OPENAI_API_KEY=sk-your-openai-key

# Upstash Redis
UPSTASH_REDIS_REST_URL=https://your-redis.upstash.io
UPSTASH_REDIS_REST_TOKEN=your-token
REDIS_PREFIX=docusummarize

# Google Drive
NEXT_PUBLIC_GOOGLE_CLIENT_ID=your-client-id.apps.googleusercontent.com
GOOGLE_API_KEY=your-api-key

# API URL (for frontend)
NEXT_PUBLIC_API_URL=http://localhost:8000

# Railway (for production)
RAILWAY_PUBLIC_DOMAIN=your-domain.railway.app
```

### 3️⃣ Install Dependencies

**Backend:**
```bash
pip install -r api/requirements.txt
```

**Frontend:**
```bash
cd web
npm install
```

### 4️⃣ Database Setup

Run the Supabase migration:
```sql
-- Create schema
CREATE SCHEMA IF NOT EXISTS docusummarize;

-- Create messages table
CREATE TABLE docusummarize.messages (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  project_id TEXT NOT NULL,
  role TEXT NOT NULL,
  content TEXT,
  meta JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Create jobs table
CREATE TABLE docusummarize.jobs (
  id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
  project_id TEXT NOT NULL,
  kind TEXT,
  status TEXT,
  payload JSONB,
  result JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Create indexes
CREATE INDEX idx_messages_project ON docusummarize.messages(project_id);
CREATE INDEX idx_messages_created ON docusummarize.messages(created_at DESC);
CREATE INDEX idx_jobs_project ON docusummarize.jobs(project_id);
```

### 5️⃣ Run Locally

**Start Backend (Terminal 1):**
```bash
uvicorn api.main:app --reload --host 0.0.0.0 --port 8000
```

**Start Frontend (Terminal 2):**
```bash
cd web
npm run dev
```

**Open in Browser:**
```
http://localhost:3000
```

---

## 🧪 Testing

### Run Backend Tests
```bash
pip install pytest
pytest api/tests/
```

### Test Coverage
```bash
pytest --cov=api api/tests/
```

### Smoke Tests
All 6 core tests passing! ✅
- ✅ Run agent and poll job
- ✅ Chunk text with overlap
- ✅ Redis JSON operations
- ✅ Supabase message persistence
- ✅ OpenAI adapter integration
- ✅ Rate limiting (60s bucket)

---

## 📚 API Documentation

### 🔹 POST `/agent/run`
Start a summarization or analysis job.

**Request:**
```json
{
  "projectId": "demo-project",
  "input": "Focus on financial metrics",
  "files": [
    {
      "id": "local-abc123",
      "name": "report.pdf",
      "mimeType": "application/pdf",
      "text": "..."
    }
  ],
  "mode": "summarize"
}
```

**Response:**
```json
{
  "id": "job-uuid",
  "status": "queued"
}
```

---

### 🔹 GET `/jobs/{job_id}`
Poll job status and get result.

**Response (Processing):**
```json
{
  "id": "job-uuid",
  "status": "running",
  "result": null,
  "error": null
}
```

**Response (Complete):**
```json
{
  "id": "job-uuid",
  "status": "done",
  "result": {
    "text": "# Overview\n...",
    "meta": {
      "tokens": {"input": 1234, "output": 567},
      "files": [...],
      "citations": [...]
    }
  },
  "error": null
}
```

---

### 🔹 GET `/messages?projectId=demo-project`
Get message history for a project.

**Response:**
```json
{
  "projectId": "demo-project",
  "messages": [
    {
      "id": "msg-uuid",
      "project_id": "demo-project",
      "role": "assistant",
      "content": "# Overview\n...",
      "meta": {
        "files": [...],
        "tokens": {...}
      },
      "created_at": "2025-11-03T14:23:45Z"
    }
  ]
}
```

---

### 🔹 POST `/upload`
Upload local files and extract text.

**Request:** `multipart/form-data` with file(s)

**Response:**
```json
{
  "files": [
    {
      "id": "local-uuid",
      "name": "document.pdf",
      "mimeType": "application/pdf",
      "text": "Extracted text content..."
    }
  ]
}
```

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

## 🚀 Deployment

### Deploy to Railway

1. **Create Railway Account** at [railway.app](https://railway.app)

2. **Connect GitHub Repo**
   - Import project from GitHub
   - Railway auto-detects `railway.toml`

3. **Add Environment Variables**
   - Copy all variables from `.env`
   - Add to Railway dashboard

4. **Deploy**
   - Railway builds 2 services: `api` and `web`
   - Auto-generates domains

5. **Update CORS**
   - Set `RAILWAY_PUBLIC_DOMAIN` to web URL
   - Redeploy API

### Deploy to Vercel (Alternative)

```bash
cd web
vercel --prod
```

Set environment variables in Vercel dashboard.

---

## 📁 Project Structure

```
ai-document-summarizer-pro/
├── 📁 api/                      # FastAPI backend
│   ├── 📁 adapters/            # OpenAI adapter
│   │   └── openai_adapter.py  # Summarization & analysis
│   ├── 📁 services/            # External services
│   │   └── external.py        # Drive API stub
│   ├── 📁 tests/               # Pytest tests
│   │   └── test_smoke.py      # Core tests
│   ├── main.py                # FastAPI app & routes
│   └── requirements.txt       # Python dependencies
│
├── 📁 web/                      # Next.js frontend
│   ├── 📁 app/                 # App router pages
│   │   ├── page.tsx           # Homepage
│   │   ├── dashboard/         # Dashboard page
│   │   └── playground/        # Playground page
│   ├── 📁 components/          # React components
│   │   ├── Hero.tsx           # Landing hero
│   │   ├── TopBar.tsx         # Navigation
│   │   ├── Footer.tsx         # Footer
│   │   └── BottomNav.tsx      # Mobile nav
│   ├── 📁 hooks/               # Custom hooks
│   │   └── useAgent.ts        # API integration
│   ├── 📁 public/              # Static assets
│   │   └── 📁 icons/          # File type icons
│   └── package.json           # Node dependencies
│
├── 📁 docs/                     # Documentation
│   ├── DASHBOARD_FEATURE.md   # Dashboard guide
│   ├── DASHBOARD_WIRING.md    # Data flow docs
│   └── EXCEL_ANALYSIS_FEATURE.md
│
├── 📁 .cursor/rules/            # AI agent rules
│
├── .env                        # Environment variables
├── .env.example               # Environment template
├── railway.toml               # Railway config
├── README.md                  # This file
└── LICENSE                    # MIT License
```

---

## 🔧 Advanced Configuration

### Redis Keys
- `docusummarize:job:{id}` - Job state/result
- `docusummarize:rate:{bucket}` - Rate limiting (60s)
- `docusummarize:cache:doc:{docId}` - Document cache

### Rate Limiting
Simple 60s token bucket on sensitive routes. Adjust in `api/main.py`:

```python
RATE_LIMIT = 10  # requests per bucket
BUCKET_DURATION = 60  # seconds
```

### File Size Limits
- **Excel/CSV**: 5MB max, 500 rows
- **PDF/Word/Text**: 10MB recommended

Adjust in `api/main.py`:

```python
MAX_FILE_SIZE = 5 * 1024 * 1024  # 5MB
MAX_ROWS = 500
```

---

## 🐛 Troubleshooting

### Common Issues

**❌ "API developer key is invalid"**
- Check Google Cloud Console
- Ensure API key restrictions allow your domain
- Enable Google Drive API & Picker API

**❌ "Access blocked: verification required"**
- Add test users in OAuth consent screen
- Go to "Audience" section
- Add email addresses

**❌ "404: This page could not be found"**
- Check `NEXT_PUBLIC_API_URL` is set correctly
- Ensure API server is running
- Verify CORS settings

**❌ Empty dashboard**
- Process a document in Playground first
- Check Supabase connection
- Verify schema name (`docusummarize`)

**❌ Build errors**
- Clear Next.js cache: `rm -rf .next`
- Reinstall dependencies: `npm install`
- Check Node version: `node --version` (18+)

---

## 📈 Performance

### Benchmarks
- **Summarization**: ~3-8s for 10-15 page docs
- **Analysis**: ~4-10s for 500-row datasets
- **p95 latency**: <8s (with caching)

### Optimization Tips
1. Enable Redis caching for repeated documents
2. Use chunking for large files
3. Adjust OpenAI model (GPT-4 vs GPT-3.5)
4. Implement CDN for static assets

---

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

### Development Guidelines
- Follow existing code style
- Add comments for complex logic
- Update documentation
- Test thoroughly

---

## 🛣️ Roadmap

### v1.1 (Planned)
- [ ] Real-time updates (WebSocket)
- [ ] Pagination for dashboard
- [ ] Export to PDF/DOCX
- [ ] Bulk operations
- [ ] Custom AI models

### v2.0 (Future)
- [ ] Multi-user authentication
- [ ] Team workspaces
- [ ] Advanced analytics charts
- [ ] API rate limiting UI
- [ ] Webhook integrations

---

## 📜 License

MIT License - see [LICENSE](LICENSE) file for details.

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
