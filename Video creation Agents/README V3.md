# 🎬 KIE Veo3 Video Generation → YouTube Upload (n8n Workflow)

## Overview

This n8n workflow automates **video publishing to YouTube** from two sources:

1. **KIE Veo3–generated videos** (via API)
2. **Existing videos stored in Google Drive**

It is designed for creators, coaches, and educators who want to:
- Generate AI videos
- Fetch them as binary data
- Upload them to YouTube automatically (as **Private** by default)

---

## 🧩 What This Workflow Does

### Flow 1: KIE Veo3 → YouTube
1. Collects video metadata via a **Form Trigger**
2. Fetches video details from the **KIE Veo3 API**
3. Downloads the generated MP4 as **binary**
4. Uploads the video to **YouTube (Private)**

### Flow 2: Google Drive → YouTube
1. Collects metadata via a **Form Trigger**
2. Downloads an MP4 from **Google Drive**
3. Uploads the video to **YouTube (Private)**

---

## 🏗️ Workflow Architecture

### KIE Veo3 Path
Form Trigger (Through Kie Video)  
→ HTTP Request – Get Video Info (KIE API)  
→ HTTP Request – Download MP4 (Binary)  
→ YouTube – Upload Video (Private)

### Google Drive Path
Form Trigger (Through Google Drive)  
→ Google Drive – Download File (Binary)  
→ YouTube – Upload Video (Private)

---

## 📌 Nodes Explained

### Through Kie Video (Form Trigger)
Collects:
- Prompt (used as YouTube title)
- Aspect Ratio
- Model (veo3_fast / fast)
- Description (used as YouTube description)

---

### Download Video from VEO3 (HTTP Request)
- Calls KIE API endpoint  
- Uses `taskId` to fetch video metadata
- Authenticated via **Header Auth (KIE API key)**

Output: JSON containing video download URL

---

### Get Binary Data from Video (HTTP Request)
- Downloads the MP4 from KIE
- Response format: **File**
- Produces binary output (`video/mp4`)

---

### Upload a video (YouTube Node)
- Uploads the downloaded video
- Title: Prompt from form
- Description: Form description
- Privacy: `private`
- Category: Education

---

## 🔐 Credentials Required

- KIE API (HTTP Header Auth)
- Google Drive OAuth2
- YouTube OAuth2 (youtube.upload scope)

---

## 🧪 Testing

1. Activate workflow
2. Open a Form Trigger URL
3. Submit inputs
4. Verify execution
5. Check YouTube Studio (Private videos)

---

## 🚀 Recommended Enhancements

- Auto-publish after approval
- Retry logic if video not ready
- Backup videos to Google Drive
- AI-generated titles & descriptions

---

## 📄 File

Workflow JSON:
SG_2March_Veo3_KIE_Video_Generation_V3_YoutubePost.json
