# 🎬 KIE VEO3 Video Generation – n8n Workflows (V1 & V2)

This repository contains **two production-ready n8n workflows** to generate short AI videos using **KIE VEO3** and automatically store the output in **Google Sheets**.

- **V1** – Developer / internal testing workflow  
- **V2** – No‑code, form-based workflow for teams & communities

---

## 🧩 What Problem This Solves

Creating short AI videos usually involves:
- Writing prompts
- Calling video generation APIs
- Waiting for async rendering
- Fetching the final video URL
- Manually tracking outputs

These workflows **fully automate** the above using n8n.

---

## 📦 Files Included

| File | Purpose |
|---|---|
| `SG_2March_Veo3_KIE_Video_Generation_V1.json` | Manual / developer-driven workflow |
| `SG_2March_Veo3_KIE_Video_Generation_V2_Form.json` | Form-triggered workflow for non-technical users |

---

## 🧠 Key Use Cases

### 🔹 Content Creators
- Generate Instagram Reels / YouTube Shorts from prompts
- Track all generated videos in Google Sheets

### 🔹 Coaches & Communities
- Give students a form to generate AI videos
- No API exposure, no technical setup

### 🔹 Internal Teams
- Rapid prompt testing for video ideas
- Centralized output logging

---

## ⚙️ Common Architecture (V1 & V2)

```
Trigger
  ↓
Generate Video (VEO3 API)
  ↓
Wait for Rendering (30s)
  ↓
Fetch Video URL
  ↓
Save Output to Google Sheets
```

---

## 🚀 Workflow V1 – Manual / Developer Version

### 🔍 Best For
- Testing prompts
- Developers
- Internal automation

### 🔑 Trigger
- **Manual Trigger** (Execute Workflow)

### 🧱 Step-by-Step Flow

1. **Manual Trigger**
   - Start the workflow manually

2. **Edit Fields (Set Node)**
   - Define:
     - `prompt`
     - `aspect ratio` (9:16 or 16:9)
     - `model` (e.g. `veo3_fast`)

3. **Generate Video with VEO3**
   - POST request to:
     ```
     https://api.kie.ai/api/v1/veo/generate
     ```
   - Returns `taskId`

4. **Wait (30 seconds)**
   - Allows video rendering to complete

5. **Download Video from VEO3**
   - GET request using `taskId`
   - Retrieves final video URL

6. **Save to Google Sheets**
   - Stores:
     - Title
     - Video status
     - Video link

---

## 🚀 Workflow V2 – Form-Based (No Code)

### 🔍 Best For
- Communities
- Students
- Non-technical users

### 🔑 Trigger
- **n8n Form Trigger**

### 🧾 Form Fields
- **Prompt** (text)
- **Aspect Ratio** (9:16 / 16:9)
- **Model** (`veo3_fast`, `fast`)

### 🧱 Step-by-Step Flow

1. **User Submits Form**
   - Prompt + settings captured

2. **Generate Video with VEO3**
   - Uses form inputs dynamically

3. **Wait (30 seconds)**
   - Ensures rendering completion

4. **Download Video from VEO3**
   - Fetches video URL

5. **Save to Google Sheets**
   - Auto-maps:
     - Prompt → Title
     - Status
     - Video URL

✅ Zero API exposure  
✅ Fully self-serve  
✅ Scales to large audiences

---

## 🔐 Credentials Required

| Service | Credential Type |
|---|---|
| KIE VEO3 | HTTP Header Auth |
| Google Sheets | OAuth2 |

---

## 📊 Output Example (Google Sheets)

| Title | Video Status | Video Link |
|---|---|---|
| Army of ants parade | success | https://...mp4 |

---

## 🧠 V1 vs V2 – Quick Comparison

| Feature | V1 | V2 |
|---|---|---|
| Trigger | Manual | Form |
| User Friendly | ❌ | ✅ |
| Prompt Editing | Set Node | UI Form |
| Community Ready | ❌ | ✅ |

---

## 🛠 Customization Ideas

- Add **caption generation**
- Auto-publish to Instagram / YouTube
- Add retry logic for failed renders
- Add approval step before publishing

---

## ✅ Final Notes

- V1 is ideal for **builders**
- V2 is ideal for **scale**
- Both workflows are production-safe and extensible

If you're teaching AI agents, automation, or content systems — **V2 is your power move**.

Happy automating 🚀
