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

`phase-3-visitor-counter` 

---

### ✅ Folder Structure

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

---


