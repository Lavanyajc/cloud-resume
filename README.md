# cloud-resume-challenge
My Cloud Resume Challenge project

| CRC Phase  | Task                                                         | Status            |
| ---------- | -----------------------------------------------------------  | ----------------- |
| ✅ Phase 1  | HTML Resume + GitHub Pages                                  | Done              |
| ✅ Phase 2  | Custom Domain (`luffyjc.xyz`)                               | Done              |
| ✅ Phase 3  | Visitor Counter API (Go + Render)                           | Done              |
| ✅ Phase 4 | **Frontend Integration** (connect resume to API)             | Done              |
| ✅ Phase 5 | **CI/CD** (auto-deploy HTML from GitHub via GitHub pages & render   | Done         |
| ✅ Phase 6 | **Monitoring** (UptimeRobot etc.)            |     Done    |

# Cloud Resume Challenge 🌩️ - Lavanya J C

## 🔗 Live Demo
- [Resume Website](https://www.luffyjc.xyz)


---

# 🌐 Cloud Resume Challenge — Lavanya J C

This is my implementation of the **Cloud Resume Challenge**, a real-world DevOps project designed to showcase my full-stack, cloud-native skills.

> 💡 *Due to AWS cost constraints, I used **fully free tools** to complete all phases without compromising on quality.*

---
[![Uptime Robot Status](https://img.shields.io/uptimerobot/status/m790234300-eaea3c6f2ae39f7fa5b5e9c7?label=Visitor%20Counter%20API)](https://stats.uptimerobot.com/pxgYRR0FOn)

🔗 **Live Status Page**: [https://stats.uptimerobot.com/pxgYRR0FOn](https://stats.uptimerobot.com/pxgYRR0FOn)


## 🚀 Live Website

📄 **Resume**: [https://lavanyajc.github.io/cloud-resume/](https://lavanyajc.github.io/cloud-resume/)

🔢 **Visitor Counter API/visits**: [https://visitor-counter-9lbd.onrender.com/visits](https://visitor-counter-9lbd.onrender.com/visits)

🔢 **Visitor Counter API/visits**: [https://visitor-counter-9lbd.onrender.com](https://visitor-counter-9lbd.onrender.com/)

---

## ✅ Project Phases

### 1. ✨ HTML/CSS Resume

* Built a professional resume using **pure HTML and CSS**
* Hosted on **GitHub Pages**
* Responsive, stylish, and includes animation, PDF download, and dark mode

### 2. 📊 Visitor Counter Backend (Go)

* Backend written in **Go (Golang)** using **Gin** framework
* Tracks visitor count using a JSON file
* Exposes a REST API at `/visits`
* Hosted via **Render** (Free Tier)

### 3. 🔄 Frontend–Backend Integration

* Connected frontend to backend using `fetch()` API
* Displays the live visitor count on the resume site

### 4. ⚙️ CI/CD (Continuous Integration/Delivery)

#### Frontend

* **GitHub Actions** CI/CD pipeline
* Automatically deploys resume to GitHub Pages on every commit

#### Backend

* **GitHub Actions** CI/CD pipeline
* Uses **Render Deploy Hook** to trigger automatic backend deployment on push

### 5. 📈 Monitoring

* Live application monitored for status and uptime
* Used:

  * **GitHub Actions status checks**
  * **Manual endpoint pinging**
  * **Browser Console Logs**
* ⚠️ Skipped tools like Grafana/Prometheus to stay within free-tier constraints

---

## 🛠️ Tools & Technologies Used

| Layer          | Tool/Service              | Purpose                              |
| -------------- | ------------------------- | ------------------------------------ |
| **Frontend**   | HTML, CSS, JS             | Resume UI                            |
|                | GitHub Pages              | Static site hosting                  |
| **Backend**    | Go, Gin                   | Visitor counter API                  |
|                | Render                    | Free backend hosting and auto deploy |
| **CI/CD**      | GitHub Actions            | CI/CD for both frontend & backend    |
|                | Render Deploy Hook        | Auto deploy Render backend on commit |
| **DNS**        | GoDaddy                   | Custom domain (`luffyjc.xyz`)        |
| **Monitoring** | JS Logging, Manual Checks | Resume and API status monitoring     |
| **Other**      | Formspree                 | Contact form submissions             |
|                | Google Analytics          | Visitor insights and tracking        |

---

## 🧾 Project Highlights

* ✅ End-to-end **CI/CD Pipelines** using GitHub Actions and Render
* ✅ Fully **serverless & cost-free architecture**
* ✅ Integrated **visitor analytics**, **Google Analytics**, and **contact form**
* ✅ Deployed across **GitHub Pages** (Frontend) + **Render** (Backend)
* ✅ Used **clean Go code** with production practices (modular, CORS, etc.)

---

## 💸 Why No AWS?

While AWS is powerful and industry-standard, some of its services (like Lambda, API Gateway, and Route 53) can incur costs or usage limits. As a student/learner:

> I chose **cost-effective, free-tier alternatives** that simulate cloud-native architectures while allowing me to **focus on DevOps skills**.

---

## 🧠 What I Learned

* Full CI/CD pipelines using GitHub Actions
* Go web server development using Gin
* GitHub Pages deployment and CORS integration
* Render deployments and web service configurations
* Secrets management and deploy hooks
* Monitoring basics without full-blown infrastructure
* Clean HTML/CSS structure for resumes

---

## 🗂 Repo Structure

```
.github/
 └── workflows/
     └── go-ci.yml         # GitHub Actions for backend CI/CD

visitor-counter/           # Go backend API //seperate repo for clarity
 ├── main.go
 ├── counter.json
 └── go.mod

cloud-resume/              # Frontend HTML resume //seprate repo (current one)
 └── index.html
```

---

## 📞 Contact

📧 Email: [jcla9686@gmail.com](mailto:jcla9686@gmail.com)
🔗 GitHub: [@Lavanyajc](https://github.com/Lavanyajc)

---

