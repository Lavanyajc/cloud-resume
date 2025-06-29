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

- [GitHub Pages URL]( http://www.luffyjc.xyz/)
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
