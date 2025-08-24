# AI Agent for ATS Optimization 🚀

An **AI-powered workflow** built with **n8n** + **Google Gemini** to analyze job descriptions against resumes, calculate ATS match scores, identify missing keywords, and automatically optimize resumes in **LaTeX** format for better Applicant Tracking System (ATS) compatibility.

---

## 📌 Features

* **ATS Match Score** (0–100) based on exact keyword matching
* **Missing Keywords Extraction** (hard skills prioritized, then soft skills)
* **Interactive Skill Enhancement Form** to let users add additional keywords
* **AI-powered Resume Optimization** — integrates missing/added skills into LaTeX resume naturally
* **Keyword Inclusion Report** ✅❌ showing what was added vs ignored
* **Automated Email Delivery** with optimized LaTeX resume

---

## ⚙️ Tech Stack

* **[n8n]()** – Workflow automation
* **[Google Gemini (PaLM)]()** – Embeddings & LLM for ATS analysis + resume rewriting
* **Gmail API** – Sends updated resume & keyword report via email
* **LaTeX** – For structured, professional resumes

---

## 🧩 Workflow Overview

1. **Form Submission**
   * User submits job details + job description + resume (LaTeX code).
2. **ATS Match Analysis**
   * AI compares JD vs resume → calculates ATS Score → lists missing keywords.
3. **Interactive Keyword Enhancement**
   * User gets a form showing ATS score + missing skills → selects which ones to add.
4. **Resume Optimization**
   * AI rewrites the resume LaTeX code, inserting chosen skills naturally.
5. **Keyword Validation**
   * AI cross-checks included vs excluded skills → generates ✅ / ❌ report.
6. **Email Delivery**
   * Optimized resume + ATS report delivered to user’s inbox.

---

## 🔧 Setup & Installation

### Prerequisites

* [n8n]() installed (cloud or self-hosted)
* Google Gemini API key (via PaLM API)
* Gmail API credentials for sending emails
* LaTeX-compatible resume template

### Steps

1. Clone this repository:
   <pre class="overflow-visible!" data-start="2286" data-end="2408"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"><span class="" data-state="closed"></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre! language-bash"><span><span>git </span><span>clone</span><span> https://github.com/your-username/ai-agent-ats-optimization.git
   </span><span>cd</span><span> ai-agent-ats-optimization
   </span></span></code></div></div></pre>
2. Import the provided n8n workflow JSON into your n8n instance.
3. Set up credentials in n8n:
   * **Google Gemini (PaLM) API**
   * **Gmail OAuth2 API**
4. Update the workflow with your email address & recipients.
5. Deploy the workflow in n8n and test with your resume.

---

## 📊 Example Output

* **ATS Score & Missing Keywords Form**
  <pre class="overflow-visible!" data-start="2768" data-end="2884"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"><span class="" data-state="closed"></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre!"><span><span>Microsoft | </span><span>78</span><span>% | Software Engineer
  Missing Keywords: cloud computing, Java, </span><span>system</span><span> design, leadership
  </span></span></code></div></div></pre>
* **Keyword Inclusion Report**
  <pre class="overflow-visible!" data-start="2921" data-end="3039"><div class="contain-inline-size rounded-2xl relative bg-token-sidebar-surface-primary"><div class="sticky top-9"><div class="absolute end-0 bottom-0 flex h-9 items-center pe-2"><div class="bg-token-bg-elevated-secondary text-token-text-secondary flex items-center gap-4 rounded-sm px-2 font-sans text-xs"><span class="" data-state="closed"></span></div></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="whitespace-pre!"><span><span>Included Keywords:</span><span>
  </span><span>cloud</span><span></span><span>computing</span><span></span><span>✅</span><span>
  </span><span>Java</span><span></span><span>✅</span><span>

  </span><span>Not Included Keywords:</span><span>
  </span><span>system</span><span></span><span>design</span><span></span><span>❌</span><span>
  </span><span>leadership</span><span></span><span>❌</span><span>
  </span></span></code></div></div></pre>
* **Email Delivery**
  * Job details (company, position, JD link)
  * Added/removed keywords summary
  * Updated LaTeX resume code

---

## 🚀 Future Enhancements

* PDF resume auto-generation from LaTeX
* Multi-language JD parsing
* Integration with LinkedIn Jobs API
* Custom ATS scoring weights

---

## 📜 License

MIT License – Feel free to use and modify.
