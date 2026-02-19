<p align="center">
  <img src="logo.png" alt="AWS Cloud Clubs" width="280" />
</p>

<h1 align="center">☁️ AWS Cloud Clubs — Core Team Recruitment</h1>

<p align="center">
  A sleek, multi-step recruitment form for the AWS Cloud Clubs Core Team.<br/>
  No backend needed — submissions go straight to Google Sheets via Apps Script.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" />
  <img src="https://img.shields.io/badge/Google%20Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white" />
</p>

---

## ✨ Features

- 🧩 **4-Step Form** — Clean, guided multi-page flow with progress indicator
- ☁️ **Animated Clouds & Confetti** — Smooth CSS/JS animations for a polished feel
- 📱 **Fully Responsive** — Works on desktop, tablet, and mobile
- ✅ **Client-Side Validation** — Required fields, email & phone format checks
- 📊 **Google Sheets Integration** — Zero-cost, serverless data collection
- 💬 **WhatsApp Group Link** — Post-submission CTA to keep applicants in the loop

---

## 📁 Project Structure

```
├── index.html      # Multi-step form markup
├── styles.css      # All styling, animations, and responsive rules
├── script.js       # Navigation, validation, confetti, and Sheets submission
├── logo.png        # Club logo
└── README.md
```

---

## 🚀 Getting Started

1. **Clone the repo**

   ```bash
   git clone https://github.com/your-username/aws-cloud-clubs-recruitment.git
   cd aws-cloud-clubs-recruitment
   ```

2. **Open `index.html`** in your browser — that's it, no build tools needed.

3. **Connect Google Sheets** (see below) to start collecting responses.

---

## 📊 Connect Your Own Google Sheet

This is the fun part — completely free, no server required.

### 1️⃣ Create a Google Sheet

- Go to [sheets.google.com](https://sheets.google.com) and create a new spreadsheet.
- Add these headers in **Row 1**:

| A         | B          | C         | D     | E     | F      | G       | H    | I        | J            | K            | L      | M           | N          | O        |
| --------- | ---------- | --------- | ----- | ----- | ------ | ------- | ---- | -------- | ------------ | ------------ | ------ | ----------- | ---------- | -------- |
| Timestamp | First Name | Last Name | Gmail | Phone | Branch | Section | Year | Why Join | Improvements | Expectations | Skills | Other Skill | Proof Link | Workshop |

### 2️⃣ Add the Apps Script

- In your spreadsheet, go to **Extensions → Apps Script**.
- Delete any boilerplate code and paste:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);

  sheet.appendRow([
    new Date(),
    data.firstName,
    data.lastName,
    data.gmail,
    data.phone,
    data.branch,
    data.section,
    data.year,
    data.whyJoin,
    data.improvements,
    data.expectations,
    Array.isArray(data.skills) ? data.skills.join(", ") : data.skills,
    data.otherSkill,
    data.proofLink,
    data.workshop,
  ]);

  return ContentService.createTextOutput(
    JSON.stringify({ status: "success" }),
  ).setMimeType(ContentService.MimeType.JSON);
}
```

- Click **Save** (💾).

### 3️⃣ Deploy as a Web App

1. Click **Deploy → New deployment**
2. Click the gear icon → select **Web app**
3. Set:
   - **Execute as:** Me
   - **Who has access:** Anyone
4. Click **Deploy** and authorize when prompted
5. Copy the **Web App URL** — it looks like:
   ```
   https://script.google.com/macros/s/AKfycbx.../exec
   ```

### 4️⃣ Paste the URL in `script.js`

Open `script.js` and replace the placeholder:

```javascript
const GOOGLE_SHEET_URL =
  "https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec";
```

That's it — form submissions now land in your spreadsheet. 🎉

> **Tip:** If you update the Apps Script later, you need to create a **new deployment** (or update the existing one) for changes to take effect.

---

## 🛠️ Customization

| What                                | Where                               |
| ----------------------------------- | ----------------------------------- |
| Form fields & pages                 | `index.html`                        |
| Colors, fonts, animations           | `styles.css`                        |
| Validation rules & submission logic | `script.js`                         |
| WhatsApp group link                 | `index.html` → success page section |

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  Built with ☁️ by the AWS Cloud Clubs community
</p>
