# cloud-resume
My Cloud Resume Challenge project

| CRC Phase  | Task                                                         | Status            |
| ---------- | -----------------------------------------------------------  | ----------------- |
| ✅ Phase 1  | HTML Resume + GitHub Pages                                  | Done              |
| ✅ Phase 2  | Custom Domain (`luffyjc.xyz`)                               | Done              |
| ✅ Phase 3  | Visitor Counter API (Go + Render)                           | Done              |
| ✅ Phase 4 | **Frontend Integration** (connect resume to API)             | Done              |
| 🔄 Phase 5 | **CI/CD** (auto-deploy HTML from GitHub via GitHub pages & render   | Done         |
| 🔄 Phase 6 | **Monitoring** (UptimeRobot, Grafana Cloud, etc.)            |  upcoming         |

# Cloud Resume Challenge 🌩️ - Lavanya J C

## 🔗 Live Demo
- [Resume Website](https://www.luffyjc.xyz)

## 🧱 Tech Stack
- HTML/CSS (Frontend)
- Go + Gin (Backend API)
- PostgreSQL (Visitor Counter)
- Render (Backend Hosting)
- GitHub Pages / Netlify (Frontend Hosting)
- CI/CD via GitHub Actions & Render

## 🚀 Features
- ✅ Cloud-hosted resume
- ✅ Visitor counter API
- ✅ Backend in Go with database
- ✅ Full CI/CD pipeline
- ✅ Google Analytics tracking
- ✅ Contact form via Formspree
- ✅ Responsive design & dark mode

## 📊 Deployment Architecture
1. Frontend hosted via GitHub Pages/Netlify
2. Backend deployed on Render
3. Visitor count stored in `counter.json` or DB
4. CI/CD: Auto build/test/deploy using GitHub Actions

## 🛠️ How to Run Locally
```bash
git clone https://github.com/Lavanyajc/cloud-resume
cd visitor-counter
go run main.go
