# EduVault – Academic Submission & Similarity Analyzer

EduVault is a web-based Academic Submission and Similarity Analyzer that helps universities manage student assignment submissions while automatically detecting plagiarism and AI-generated content. Built as a self-hosted, open-source alternative to expensive commercial tools like Turnitin.

## 📌 Project Info

- **Domain:** Web-Based Academic Integrity Management System
- **Stack:** HTML · CSS · JavaScript · PHP · MySQL (XAMPP)

## ✨ Features

- **Multi-format uploads** – PDF, DOCX, TXT (up to 25 MB), with pure-PHP text extraction (no external binaries)
- **Plagiarism detection** – Cosine similarity on word-frequency (TF-IDF-like) vectors, comparing each submission against up to 200 prior submissions
- **AI-content detection** – Statistical analysis of sentence uniformity, burstiness, lexical diversity, and perplexity indicators (no external API required)
- **Risk classification** – Auto-flags submissions as Low (<20%), Medium (20–49%), or High (≥50%) risk
- **Role-based access** – Separate Student and Admin dashboards
- **Admin control panel** – Manage students/submissions, review flagged content, adjust thresholds, view activity logs, export CSV reports
- **Security** – bcrypt password hashing, PDO prepared statements, session regeneration, rate-limited login, input sanitization

## 🏗️ Architecture

Three-tier design:
1. **Presentation Tier** – Static HTML/CSS/JS pages, communicating via AJAX (Fetch API)
2. **Application Tier** – PHP scripts handling auth, uploads, similarity engine, AI detection, admin APIs
3. **Data Tier** – MySQL database (`eduvault`) accessed via PDO, 7 tables

## 🗄️ Database Tables

`users` · `submissions` · `similarity_matches` · `activity_log` · `courses` · `settings` · `ai_detection_results`

## 👥 User Roles

**Student:** Register, upload assignments, view similarity analysis (radar chart), run AI detection, track own submission history.

**Admin:** All student features + manage students/submissions, view system-wide KPIs, audit log, configure settings, export data.

## ⚙️ Setup (XAMPP)

1. Clone this repo into `htdocs/`
2. Start Apache + MySQL via XAMPP
3. Import the database schema via phpMyAdmin
4. Configure `php/config.php` with your DB credentials
5. Visit `php/test_connection.php` to verify the DB connection
6. Open `index.html` in your browser

## ⚠️ Known Limitations

- Compares only against submissions in its own database (no internet-wide plagiarism check)
- Similarity capped at 200 previous submissions per upload
- No email notification system yet
- No file preview/download from the UI
- AI detection is statistical only (no external API), so it may produce false positives on well-structured human writing

## 🚀 Future Enhancements

- External plagiarism API integration (Copyscape/iThenticate)
- AI detection via dedicated API (GPTZero/Originality.ai)
- Email notifications (PHPMailer/SMTP)
- In-browser file preview
- Instructor role
- Semantic similarity via SBERT embeddings
- Docker/cloud deployment
