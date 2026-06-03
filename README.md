<div align="center">

<img src="https://img.shields.io/badge/🌱-PlantWise-2d6a4f?style=for-the-badge&labelColor=1b4332" alt="PlantWise"/>

# PlantWise

### AI-Powered Plant Disease Detection & Knowledge Platform

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![Django](https://img.shields.io/badge/Django-6.0-092E20?style=flat-square&logo=django&logoColor=white)](https://www.djangoproject.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](CONTRIBUTING.md)
[![Kindwise API](https://img.shields.io/badge/Powered%20by-Kindwise%20AI-2d6a4f?style=flat-square)](https://crop.kindwise.com)

<br/>

> **Upload a leaf. Get a diagnosis. Save your crop.**
>
> PlantWise helps farmers, gardeners, and plant enthusiasts detect plant diseases instantly using AI — and share knowledge through a built-in blogging platform.

<br/>

[🚀 Quick Start](#-quick-start) · [✨ Features](#-features) · [📸 Screenshots](#-screenshots) · [🛠 Tech Stack](#-tech-stack) · [🤝 Contributing](#-contributing)

</div>

---

## ✨ Features

### 🔬 AI Plant Disease Detection
- 📷 **Upload any leaf image** — JPG, PNG supported
- 🤖 **Instant AI diagnosis** via the [Kindwise Crop API](https://crop.kindwise.com)
- 📊 **Confidence scoring** — know how certain the AI is
- 💊 **Treatment suggestions** — actionable steps to cure your plant
- 🩺 **Severity levels** — Healthy / Mild / Severe classification
- 📁 **Full diagnosis history** — every scan saved to your account

### 📝 Community Blog
- ✍️ Write and publish plant care articles
- 🗂️ Categorize posts for easy discovery
- ✏️ Full edit & delete with author-only access control
- 🌐 Public-facing blog anyone can read

### 🔐 User Accounts
- Secure registration & login
- Custom user model for future extensibility
- Profile-based diagnosis history
- Authentication-gated actions

---

## 📸 Screenshots

> _Coming soon — add your screenshots here!_

| Home | Diagnose | Result |
|------|----------|--------|
| ![home](screenshots/home.png) | ![diagnose](screenshots/diagnose.png) | ![result](screenshots/result.png) |

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Django 6.0 (Python) |
| **Database** | SQLite (dev) · Easily swappable to PostgreSQL |
| **AI / ML** | [Kindwise Crop Health API](https://crop.kindwise.com/api) |
| **Frontend** | Django Templates · HTML5 · CSS3 |
| **Auth** | Django Auth System (Custom User Model) |
| **Media** | Django file uploads · Pillow |

---

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- pip
- A free [Kindwise API key](https://crop.kindwise.com) (for disease detection)

### 1 — Clone the Repository

```bash
git clone https://github.com/Nafis-Kamal-CodeQuest/PlantWise---AI-based-plant-disease-detection-system-and-blog-website.git
cd PlantWise---AI-based-plant-disease-detection-system-and-blog-website
```

### 2 — Create a Virtual Environment

```bash
python -m venv venv

# macOS / Linux
source venv/bin/activate

# Windows
venv\Scripts\activate
```

### 3 — Install Dependencies

```bash
pip install django pillow requests
```

### 4 — Configure Environment Variables

Create a `.env` file in the project root:

```env
KINDWISE_API_KEY=your_api_key_here
KINDWISE_API_URL=https://crop.kindwise.com/api/v1
SECRET_KEY=your-secret-django-key-here
```

> 🔑 Get your free Kindwise API key at [crop.kindwise.com](https://crop.kindwise.com)

### 5 — Apply Migrations & Run

```bash
python manage.py migrate
python manage.py createsuperuser   # optional, for admin access
python manage.py runserver
```

Visit **http://127.0.0.1:8000** 🎉

---

## 📁 Project Structure

```
PlantWise/
│
├── accounts/          # Custom user model, registration & login
│   ├── models.py      # CustomUser (extends AbstractUser)
│   ├── views.py
│   └── urls.py
│
├── blog/              # Community blog platform
│   ├── models.py      # Post model (title, content, category, author)
│   ├── views.py       # Full CRUD with author-only access control
│   └── templates/blog/
│
├── core/              # Homepage & shared navigation
│   └── templates/core/
│
├── detector/          # 🌟 AI Disease Detection engine
│   ├── models.py      # DiagnosisResult model
│   ├── views.py       # Upload → API → Result flow
│   ├── utils.py       # Kindwise API integration
│   └── templates/detector/
│
├── plantwise/         # Django project config
│   ├── settings.py
│   └── urls.py
│
├── templates/         # Global base templates
├── manage.py
└── .env               # ← Create this (see setup)
```

---

## 🔌 How the AI Detection Works

```
User uploads leaf image
        │
        ▼
Image encoded to base64
        │
        ▼
POST → Kindwise Crop API
        │
        ▼
Parse JSON response:
  ├── Disease name
  ├── Confidence score
  ├── Description
  ├── Treatment plan
  └── Severity level
        │
        ▼
Save DiagnosisResult to DB
        │
        ▼
Render result to user
```

The API call is handled in `detector/utils.py`, and the full flow including error handling lives in `detector/views.py`.

---

## 🌐 URL Routes

| URL | View | Description |
|-----|------|-------------|
| `/` | `core.home` | Homepage |
| `/blog/` | `blog.blog_list` | All blog posts |
| `/blog/<id>/` | `blog.post_detail` | Single post |
| `/blog/create/` | `blog.post_create` | New blog post |
| `/detection/diagnose/` | `detector.diagnose_plant` | Upload & detect |
| `/detection/result/<id>/` | `detector.diagnosis_result` | Diagnosis result |
| `/detection/history/` | `detector.history` | User's scan history |
| `/accounts/register/` | `accounts.register` | Registration |
| `/login/` | Django built-in | Login |
| `/admin/` | Django Admin | Admin panel |

---

## ⚙️ Configuration Reference

All settings are loaded from environment variables (via `.env`):

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `SECRET_KEY` | ✅ | — | Django secret key |
| `KINDWISE_API_KEY` | ✅ | — | Your Kindwise API key |
| `KINDWISE_API_URL` | ❌ | `https://crop.kindwise.com/api/v1` | Kindwise base URL |
| `DEBUG` | ❌ | `True` | Debug mode |

---

## 🔮 Roadmap

- [ ] Switch to PostgreSQL for production
- [ ] Add image preview before upload
- [ ] Blog post cover images
- [ ] Comment system for blog posts
- [ ] REST API (DRF) for mobile app integration
- [ ] Email notifications for diagnosis
- [ ] Multi-language support
- [ ] Docker + deployment guide

---

## 🤝 Contributing

Contributions are welcome! Here's how to get involved:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

Please make sure your code follows Django best practices and includes relevant tests.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgements

- [Kindwise](https://kindwise.com) for their powerful plant health API
- [Django](https://djangoproject.com) for the robust web framework
- All contributors and testers 🌿

---

<div align="center">

Made with ❤️ and 🌱 by [Nafis Kamal](https://github.com/Nafis-Kamal-CodeQuest)

⭐ **Star this repo if you found it helpful!**

</div>
