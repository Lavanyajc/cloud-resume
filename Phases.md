## ✅ Phase 1: HTML Resume + GitHub Pages

📁 **Folder Structure**

```
phase-1-html-resume/
├── index.html
└── README.md
```

📄 **index.html**
 existing file in repo


📄 **README.md**

```md
# 🌐 Phase 1: HTML Resume + GitHub Pages

## ✅ What I Did

- Created a `cloud-resume` repository on GitHub.
- Built a resume using **HTML** with inline CSS styles (embedded in `<style>` tag).
- Used a responsive layout with custom themes (light/dark mode).
- Added animation, project cards, skills, contact form (Formspree), and analytics (Google Analytics).
- Hosted the resume using **GitHub Pages**.

## 🚀 Deployment Steps

1. Went to GitHub repository → Settings → Pages.
2. Selected:
   - **Branch**: `main`
   - **Folder**: `/ (root)`
3. Did **NOT rename repo** to `username.github.io` — used default repo name (`cloud-resume`).
4. GitHub gave me a GitHub Pages URL that rendered my resume.

## 🔗 Live Link

- [GitHub Pages URL](https://www.luffyjc.xyz/)
```

---

## ✅ Phase 2: Custom Domain Mapping (GoDaddy)

📁 **Folder Structure**

```
phase-2-custom-domain/
└── README.md
```

📄 **README.md**

```md
# 🌐 Phase 2: Custom Domain Setup (`luffyjc.xyz`)

## ✅ What I Did

- Purchased the domain **`luffyjc.xyz`** via **GoDaddy**.
- Initially tried using Render DNS but faced issues.
- Later reverted to GoDaddy's **default nameservers**.
- Mapped this custom domain to my GitHub Pages resume.

## 🛠️ Configuration Steps

### 1. GitHub Pages Custom Domain
- Went to GitHub → Settings → Pages.
- In **Custom Domain**, entered:  
```

luffyjc.xyz

````
- GitHub auto-created a `CNAME` file in the repo.

### 2. GoDaddy DNS Setup
- Logged in to GoDaddy.
- Navigated to DNS settings.
- Added a **CNAME record**:
- **Host**: `www`
- **Points to**: `Lavanyajc.github.io`
- Also added an **A Record**:
- **Host**: `@`
- **Points to**: GitHub Pages IP:
  ```
  185.199.108.153
  185.199.109.153
  185.199.110.153
  185.199.111.153
  ```

## 📌 Outcome

- My static resume is now available at:  
🔗 **https://luffyjc.xyz**

## ⚠️ Notes

- I used the default GoDaddy name servers (not Render DNS).
- The custom domain works smoothly with GitHub Pages.
````


---

## ✅`phase-3-visitor-counter` 


📁 Folder Structure

```
phase-3-visitor-counter/
├── .github/
│   └── workflows/
│       └── go-ci.yml
├── main.go
├── go.mod
├── README.md
```

---

### 📁 `.github/workflows/go-ci.yml`

```yaml
name: Go CI/CD

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up Go
      uses: actions/setup-go@v4
      with:
        go-version: '1.20'

    - name: Build Go backend
      run: go build -v ./...

    - name: Deploy to Render using Deploy Hook
      run: |
        curl "$RENDER_DEPLOY_HOOK_URL"
      env:
        RENDER_DEPLOY_HOOK_URL: ${{ secrets.RENDER_DEPLOY_HOOK_URL }}
```

---

### 📝 `main.go`

```go
package main

import (
	"encoding/json"
	"io/ioutil"
	"net/http"
	"os"
	"sync"

	"github.com/gin-gonic/gin"
)

var mu sync.Mutex
const filePath = "counter.json"

type Counter struct {
	Visits int `json:"visits"`
}

func readCounter() Counter {
	var counter Counter
	data, err := ioutil.ReadFile(filePath)
	if err != nil {
		counter.Visits = 0
	} else {
		json.Unmarshal(data, &counter)
	}
	return counter
}

func writeCounter(counter Counter) {
	data, _ := json.Marshal(counter)
	_ = ioutil.WriteFile(filePath, data, 0644)
}

func main() {
	r := gin.Default()

	// Enable CORS
	r.Use(func(c *gin.Context) {
		c.Writer.Header().Set("Access-Control-Allow-Origin", "*")
		c.Writer.Header().Set("Access-Control-Allow-Methods", "GET, POST, OPTIONS")
		c.Writer.Header().Set("Access-Control-Allow-Headers", "Origin, Content-Type, Accept")
		if c.Request.Method == "OPTIONS" {
			c.AbortWithStatus(204)
			return
		}
		c.Next()
	})

	// API to fetch and update visit count
	r.GET("/visits", func(c *gin.Context) {
		mu.Lock()
		defer mu.Unlock()

		counter := readCounter()
		counter.Visits++
		writeCounter(counter)

		c.JSON(http.StatusOK, gin.H{
			"visits": counter.Visits,
		})
	})

	// Health check
	r.GET("/", func(c *gin.Context) {
		c.String(http.StatusOK, "Hi JC, Visitor Counter API is running!")
	})

	port := os.Getenv("PORT")
	if port == "" {
		port = "8080"
	}
	r.Run(":" + port)
}
```

---

### 📝 `go.mod`

```go
module github.com/Lavanyajc/visitor-counter

go 1.20

require github.com/gin-gonic/gin v1.10.1
```

---

### 📝 `README.md`

````markdown
# 📊 Phase 3: Visitor Counter API – Cloud Resume Challenge

This phase implements a backend service using Go (Golang) and the Gin framework to count the number of visitors to your resume.

---

## 🔧 Stack Used
- Golang (Gin)
- GitHub Actions (CI/CD)
- Render (backend hosting)
- JSON file for local storage

---

## 🔗 API Endpoint
```bash
https://visitor-counter-9lbd.onrender.com/
````

Every time your frontend calls this URL, it increments and returns the visit count.

---

## 🧪 Local Development

```bash
go mod tidy
go run main.go
```

---

## 🚀 CI/CD Pipeline

GitHub Actions automatically builds and deploys the app using a Render Deploy Hook.

---

## 📦 Files

* `main.go`: The main application file
* `go.mod`: Go module declaration
* `.github/workflows/go-ci.yml`: CI/CD pipeline configuration

```
```


## ✅ Phase 4: Frontend Integration with Visitor Counter API

### 📌 Objective:

To integrate the Go backend API (visitor counter) with the frontend HTML resume so that each time the resume is visited, the visit count is updated and displayed live.

---

### 📁 File Structure (After Integration)

```bash
cloud-resume/
├── index.html         # Main resume with integrated JS fetch for visitor count
├── CNAME              # Contains 'www.luffyjc.xyz' for custom domain mapping
├── .github/
│   └── workflows/
│       └── go-ci.yml  # For Phase 5 - CI/CD setup
```

---

### 🔗 API Used:

**Render-hosted Visitor API:**
👉 `https://visitor-counter-9lbd.onrender.com/visits`

---

### 🛠️ What I Did:

* From Phase 3, I already had a deployed Go API that returns the number of visits.
* In this phase, I opened `index.html` from my static resume and injected a script to call the above API.
* I displayed the returned visit count inside a `div` with id `visitorCount`.

---

### 📜 Code Snippet Added (in `index.html`):

```html
<div class="visitor-count" id="visitorCount">Loading visitor count...</div>

<script>
  fetch("https://visitor-counter-9lbd.onrender.com/visits")
    .then(response => response.json())
    .then(data => {
      document.getElementById("visitorCount").innerText = 
        `📈 This resume has been viewed ${data.visits} time${data.visits !== 1 ? 's' : ''}.`;
    })
    .catch(error => {
      document.getElementById("visitorCount").innerText = "⚠️ Visitor counter error";
    });
</script>
```

---

### 🧪 How I Verified:

* Deployed `index.html` via GitHub Pages.
* Visited the site using `https://luffyjc.xyz` (custom domain).
* Verified visitor count updates in real-time with every refresh.

---

### 🐞 Errors Faced & Fixes:

| Issue                                          | Fix                                                              |
| ---------------------------------------------- | ---------------------------------------------------------------- |
| **CORS Error** (`Access-Control-Allow-Origin`) | Added CORS headers in Go backend (`main.go`)                     |
| Wrong API URL used initially                   | Corrected to: `https://visitor-counter-9lbd.onrender.com/visits` |
| GitHub pages took time to reflect changes      | Committed + waited a minute, verified cache cleared              |

---

### ✅ CORS Fix in Backend:

```go
r.Use(func(c *gin.Context) {
  c.Writer.Header().Set("Access-Control-Allow-Origin", "*")
  c.Writer.Header().Set("Access-Control-Allow-Methods", "GET, POST, OPTIONS")
  c.Writer.Header().Set("Access-Control-Allow-Headers", "Origin, Content-Type, Accept")
  if c.Request.Method == "OPTIONS" {
    c.AbortWithStatus(204)
    return
  }
  c.Next()
})
```

---

### 🎯 Outcome:

* Resume now displays **real-time visitor count** on load.
* Fully integrated frontend + backend using free tools.
* Successfully bridged Phase 3 (backend) and frontend resume via JS fetch.

---


---

## 🚀 Phase 5: CI/CD – Continuous Integration & Deployment

### ✅ Goal:

Establish **fully automated deployment pipelines** for both frontend and backend:

* Frontend (`index.html`) auto-deploys via **GitHub Pages**
* Backend (`Go API`) auto-deploys to **Render** using **GitHub Actions + Deploy Hook**

---

## 🧱 Folder Structure (Post-CI/CD)

```bash
cloud-resume/                   ← HTML Resume Repository
├── index.html                  ← Resume with visitor counter integration
├── CNAME                       ← Custom domain: www.luffyjc.xyz
└── .github/
    └── workflows/
        └── pages.yml           ← (GitHub Pages manages auto-deploy — no extra file needed)

visitor-counter/                ← Backend Repository (Go API)
├── main.go                     ← Visitor counter logic
├── go.mod
├── go.sum
└── .github/
    └── workflows/
        └── go-ci.yml          ← GitHub Actions workflow for Render auto-deploy
```

---

## 🔧 What I Implemented

### ✅ **Frontend CI/CD with GitHub Pages**

* Hosted the resume as a static website.
* Configured GitHub Pages:

  * **Branch:** `main`
  * **Folder:** `/ (root)`
* Set up the custom domain: `www.luffyjc.xyz` (added in **CNAME** file).
* **Result:** Any update to `index.html` auto-publishes to the live site.

🔗 **Live Resume:** [www.luffyjc.xyz](https://www.luffyjc.xyz)

---

### ✅ **Backend CI/CD with GitHub Actions + Render Deploy Hook**

1. Deployed Go backend API to **Render**.

2. Enabled ✅ "Auto Deploy" and copied the **Render Deploy Hook URL**.

3. Added a **GitHub Secret**:

   * Name: `RENDER_DEPLOY_HOOK`
   * Value: *(Your Render deploy hook URL)*

4. Created a GitHub Actions workflow: `.github/workflows/go-ci.yml`

---

### 🧾 Final GitHub Actions Workflow

```yaml
name: Deploy Go API to Render

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      - name: 📦 Checkout Repository
        uses: actions/checkout@v3

      - name: 🔧 Setup Go
        uses: actions/setup-go@v4
        with:
          go-version: '1.21'

      - name: 🛠️ Build Go Project
        run: go build -v ./...

      - name: 🚀 Trigger Deploy on Render
        env:
          DEPLOY_HOOK: ${{ secrets.RENDER_DEPLOY_HOOK }}
        run: |
          curl -X GET "$DEPLOY_HOOK"
```

> ✅ This workflow automatically triggers deployment on Render whenever a push is made to `main`.

---

## 🔍 Verifying CI/CD Worked

| 🔁 Task                          | 🔍 Action Taken                          | ✅ Result                  |
| -------------------------------- | ---------------------------------------- | ------------------------- |
| **Frontend** auto-deploy         | Edited `index.html` → pushed to `main`   | GitHub Pages live updated |
| **Backend** auto-deploy          | Edited `main.go` → pushed to `main`      | Render auto-redeployed    |
| Confirmed via GitHub **Actions** | Green checkmarks + Deploy Hook triggered | Verified Build & Deploy   |

---

## 🧠 Issues Faced & How I Solved Them

| ⚠️ Problem                                   | 🛠️ Fix                                                                |
| -------------------------------------------- | ---------------------------------------------------------------------- |
| Deploy hook wasn’t working                   | Used correct Render URL, added secret properly                         |
| GitHub Actions failed on build step          | Ensured `go.mod` and `main.go` were working with `go build`            |
| Auto-deploy didn’t trigger on update         | Verified branch was `main`, and deploy secret was valid                |
| Confused between `pages.yml` and `go-ci.yml` | Used GitHub Pages' native deployment (no workflow needed for frontend) |

---

## 🎯 Outcome

✨ **CI/CD success for both front and back ends**:

* ✅ Frontend: GitHub Pages handles resume deployment automatically
* ✅ Backend: Render redeploys instantly via GitHub Actions + Deploy Hook
* 🔄 I just push code — and **everything goes live automatically**

---

## 🛠️ Tools & Services Used

| Tool                   | Purpose                                     |
| ---------------------- | ------------------------------------------- |
| **GitHub Pages**       | Frontend hosting + automatic static deploy  |
| **Render**             | Backend hosting for Go API                  |
| **GitHub Actions**     | CI/CD pipelines for backend auto-deployment |
| **Go** (Golang)        | Backend API for visitor counter             |
| **Git** & **Git Bash** | Version control & CLI operations            |

---


---

## ✅ Phase 6 – Monitoring (Free, Lightweight & Effective)

To complete the Cloud Resume Challenge with a solid DevOps touch, I implemented **real-time monitoring** to ensure my backend API remains available 24/7.

### 🚀 What I Implemented

I used **UptimeRobot** (a free and reliable uptime monitoring tool) to monitor my deployed **Go backend visitor counter API**.

* ✅ **Monitored URL**: [`https://visitor-counter-9lbd.onrender.com/`](https://visitor-counter-9lbd.onrender.com/)
* ✅ **Monitor Type**: HTTP(s)
* ✅ **Check Frequency**: Every 5 minutes
* ✅ **Alerting**: Email notifications on downtime

This setup ensures I get **instant alerts** if the API becomes unreachable — keeping me proactive about service reliability.

### 🎯 Why UptimeRobot?

* 💸 **100% Free** — perfectly aligned with my zero-cost CRC goal.
* ⚡ **No infrastructure overhead** — no need to host or manage Grafana/Prometheus.
* 🧠 **Smart DevOps decision** — simple, scalable, and production-ready for lightweight projects.

### ✅ Outcome

* My API’s availability is continuously tracked.
* I receive alerts if the service goes down, enabling rapid recovery.
* This completes the **DevOps loop** of build → deploy → monitor.

> 📈 With monitoring in place, my CRC project is not just complete — it's production-aware and reliable.

---

