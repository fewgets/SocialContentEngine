<!-- Social Content Engine · README by Usama Shahid (fewgets) -->
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,55:0F3D3E,100:36FFC7&height=230&section=header&text=Social%20Content%20Engine&fontSize=50&fontColor=FFFFFF&fontAlignY=36&desc=Drive%20to%20Instagram%2C%20fully%20automated%20with%20AI%20captions&descSize=17&descAlignY=58&animation=fadeIn" width="100%" alt="Social Content Engine"/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=700&color=36FFC7&center=true&vCenter=true&width=720&height=60&lines=Google+Drive+to+Instagram;AI-Written+Captions+and+Hashtags;Zero+Duplicates%2C+Zero+Effort" alt="Typing SVG"/>

<p>
  <img src="https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white" alt="n8n"/>
  <img src="https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white" alt="OpenAI"/>
  <img src="https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white" alt="Supabase"/>
  <img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram"/>
  <img src="https://img.shields.io/badge/Google%20Drive-4285F4?style=for-the-badge&logo=googledrive&logoColor=white" alt="Google Drive"/>
</p>

</div>

---
## 📌 Overview

**Social Content Engine** is an **n8n** automation that runs your Instagram for you. Drop images
into a Google Drive folder and the workflow does the rest:

> 📂 finds new images → 🔁 skips anything already posted → ☁️ uploads to Supabase Storage →
> ✍️ writes a caption and hashtags with **OpenAI** → 📸 publishes to **Instagram** → 🗂️ logs the post.

---

## 🎥 Workflow

<p align="center">
  <img src="Images/flow.png" alt="n8n workflow" width="90%"/>
</p>

---

## ✨ Features

| | Feature | Details |
|:-:|---|---|
| 📂 | **Google Drive source** | Watches a folder for new images |
| 🔁 | **No duplicates** | Every posted file is recorded in Supabase and skipped next time |
| ☁️ | **Public image hosting** | Uploads to a Supabase Storage bucket and generates a public URL |
| ✍️ | **AI captions** | `gpt-4o-mini` looks at the image and writes a caption with hashtags |
| 📸 | **Auto-publish** | Creates and publishes Instagram media through the Facebook Graph API |
| ⏱️ | **Scheduled** | Runs automatically, no manual steps |

---

## 🔄 How It Works

```mermaid
flowchart LR
    D[📂 Google Drive<br/>new images] --> C{Already<br/>posted?}
    C -->|Yes| X[⏭️ Skip]
    C -->|No| U[☁️ Upload to<br/>Supabase Storage]
    U --> AI[✍️ OpenAI<br/>caption + hashtags]
    AI --> IG[📸 Instagram<br/>Graph API]
    IG --> L[(🗂️ Log in Supabase)]
```

---

## 📷 Example Output

<p align="center">
  <img src="Images/example_post.png" alt="Example Instagram post" width="420"/>
</p>

---

## ⚙️ Setup

### ✅ Prerequisites
- A running **n8n** instance (self-hosted or cloud)
- **Google Drive API** with OAuth2 credentials
- A **Supabase** project
- A **Facebook App** linked to a Page and an Instagram **Business/Creator** account
- An **OpenAI** API key

### 1. Google Drive
Enable the Drive API, create OAuth2 credentials (redirect: `/rest/oauth2-credential/callback`) and
set your folder ID in the search node:
```text
'YOUR_FOLDER_ID' in parents and mimeType contains 'image/'
```

### 2. Supabase
Create a **public** storage bucket named `insta_uploads` and this table:
```sql
create table public.my_table (
  id         text primary key,
  name       text not null,
  created_at timestamptz default now()
);
```

### 3. OpenAI
Add your API key to the **OpenAI** node (model `gpt-4o-mini`).

### 4. Instagram / Facebook Graph API
Generate a Page access token with `instagram_content_publish`, then get your Instagram Business ID:
```text
GET /{page-id}?fields=instagram_business_account
```

### 5. Import and run
Import `Social Media Post.json` into n8n, connect the credentials, test node by node, then **activate**.

---

## 🧰 Tech Stack

| Component | Tool |
|---|---|
| Automation | [n8n](https://n8n.io) |
| Source | Google Drive |
| Database and Storage | Supabase (PostgreSQL + Storage) |
| AI Captions | OpenAI `gpt-4o-mini` |
| Publishing | Facebook Graph API (Instagram) |

---

## 🤝 Let's Work Together

<div align="center">

**Have an idea, a freelance project, or want to collaborate on something in AI?**
I'm always open to collaborations, freelance work and full-time opportunities.

<a href="mailto:shaikhusama541@gmail.com?subject=Collaboration%20-%20Social%20Content%20Engine">
  <img src="https://img.shields.io/badge/Email-shaikhusama541%40gmail.com-36FFC7?style=for-the-badge&logo=gmail&logoColor=white&labelColor=0D1117" alt="Email"/>
</a>
<a href="https://www.linkedin.com/in/-usamashahid/">
  <img src="https://img.shields.io/badge/LinkedIn-Usama%20Shahid-36FFC7?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=0D1117" alt="LinkedIn"/>
</a>
<a href="https://github.com/fewgets">
  <img src="https://img.shields.io/badge/GitHub-fewgets-36FFC7?style=for-the-badge&logo=github&logoColor=white&labelColor=0D1117" alt="GitHub"/>
</a>

<br/><br/>

⭐ **If you like this project, please give it a star. It really helps!** ⭐

<br/>

<h3>"Create once. Let automation do the posting."</h3>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:36FFC7,55:0F3D3E,100:0D1117&height=150&section=footer&animation=twinkling" width="100%" alt="footer"/>

</div>
