# VulnLab — Intentionally Vulnerable Demo Sites

> ⚠️ **Educational use only.** All vulnerabilities are intentional and simulated client-side. No real database, no real file uploads, no real money transfers.

4 standalone HTML/JS sites for security training, each deployable as its own Vercel project.

---

## Sites

| Folder | Site | Vulnerability |
|--------|------|---------------|
| `sqli-bank/` | **SQLi Bank** | SQL Injection |
| `reflectx-xss/` | **ReflectX** | Reflected XSS |
| `uploadpwn/` | **UploadPwn** | Unrestricted File Upload |
| `transfergo-csrf/` | **TransferGo** | CSRF |

---

## Deploy to Vercel (each site is its own project)

### Option A — Vercel CLI (fastest)

```bash
npm i -g vercel

# Deploy each folder as a separate project
cd sqli-bank       && vercel --prod && cd ..
cd reflectx-xss    && vercel --prod && cd ..
cd uploadpwn       && vercel --prod && cd ..
cd transfergo-csrf && vercel --prod && cd ..
```

Each command gives you a live `*.vercel.app` URL.

### Option B — Vercel Dashboard (UI)

1. Go to [vercel.com/new](https://vercel.com/new)
2. Import this GitHub repo
3. Set **Root Directory** to one of the 4 folders
4. Click **Deploy**
5. Repeat for each folder as a separate project

---

## Site Details

### 1. SQLi Bank (`sqli-bank/`)
- Fake banking login with a hardcoded user table shown on screen
- Live SQL query monitor updates as you type
- Payload: `' OR '1'='1` in the username field bypasses auth
- Collapsible vuln panel explains the issue + parameterised query fix

### 2. ReflectX (`reflectx-xss/`)
- Fake search engine reflecting user input via `innerHTML`
- Click-to-inject XSS payload chips (`<img src=x onerror=alert('XSS')>` etc.)
- **Safe Mode toggle** switches to `textContent` to show the fix side-by-side
- Collapsible vuln panel with DOMPurify fix example

### 3. UploadPwn (`uploadpwn/`)
- Fake image hosting that accepts any file type with no validation
- Real drag-and-drop UI with simulated upload progress bar
- Uploaded filename appears in a live `/uploads/` directory listing
- Pre-planted `shell.php` demonstrates what an attacker would leave behind
- Collapsible vuln panel explains MIME validation + storing outside web root

### 4. TransferGo (`transfergo-csrf/`)
- Fake money transfer app with localStorage-based "session"
- Transfer form has **no CSRF token**
- `attacker.html` — a fake "you've won a prize" phishing page that:
  - Shows the CSRF attack step-by-step
  - Auto-submits a hidden form and postMessages the result back
  - The balance on `index.html` updates in real time to show $9,999 stolen
- Collapsible vuln panel explains CSRF tokens + SameSite cookies

---

## File Structure

```
vulnerablesites/
├── sqli-bank/
│   ├── index.html
│   └── vercel.json
├── reflectx-xss/
│   ├── index.html
│   └── vercel.json
├── uploadpwn/
│   ├── index.html
│   └── vercel.json
├── transfergo-csrf/
│   ├── index.html      ← victim app
│   ├── attacker.html   ← malicious CSRF page
│   └── vercel.json
└── README.md
```
