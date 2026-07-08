# Linkedin-Auto-Poster
*Telegram → AI Draft → Human Approval → LinkedIn Publish*

> "What if you could turn a voice note or a quick Telegram message into a polished, on-brand LinkedIn post — without opening a blank doc and staring at it for 20 minutes?"

---

## The Story

If you've ever tried to "post consistently" on LinkedIn, you know the real problem isn't ideas — it's friction. You have a thought in the shower, in traffic, or right after a client call... and by the time you sit down to write it up, the moment (and the motivation) is gone.

For business owners, consultants, and educators trying to build a presence, this usually means either skipping the post entirely, or spending way more time than it deserves formatting and second-guessing the wording.

So I built a workflow that lets me capture the idea the moment I have it — straight from Telegram — and have AI turn it into a properly structured LinkedIn post, ready for me to approve and publish, with zero copy-pasting between apps.

This is that build.

---

## 🎯 The Problem

- Good content ideas get lost between "I should post this" and actually opening LinkedIn.
- Writing a post that's structured (hook, story, lesson, CTA) takes real effort every single time — even when you know the formula.
- Publishing directly to LinkedIn from outside their app isn't as simple as pasting text; it requires API authentication most beginners have never touched.
- The cost of skipping all this? Inconsistent posting, and inconsistent posting is the #1 killer of a growing personal brand.

---

## ⚙️ The Solution

Here's what this automation does, step by step:

1. **Trigger** — I send a message to a dedicated Telegram bot with my raw idea (a rough thought, a story, a lesson learned that day).
2. **Process** — The message is passed to an AI model (Gemini, with Groq as a backup when rate limits hit) which drafts a full LinkedIn post following a set structure: hook → story → lesson → engagement question → hashtags.
3. **Human-in-the-loop** — The AI draft is sent back to me in Telegram before anything goes live. I can approve it, edit it, or reject it — nothing publishes without my say-so.
4. **Act** — Once approved, the workflow calls LinkedIn's UGC (User Generated Content) API and publishes the post directly to my personal profile.

> 💡 Beginner note: "UGC API" just means the specific LinkedIn endpoint built for posting content on someone's behalf — think of it as the door n8n knocks on to say "publish this post for this person." LinkedIn requires you to prove *who* you are before it lets you through that door, which is where the authentication setup comes in.

---

## Tools Used

| Tool | Role in this workflow |
|------|------------------------|
| n8n | Orchestration / workflow engine |
| Telegram | Capture ideas on the go + human approval step |
| Gemini | Drafts the post from a raw idea |
| LinkedIn UGC API | Publishes the final approved post to my personal profile |

---

##  Demo

<img width="729" height="327" alt="image" src="https://github.com/user-attachments/assets/ac665a6a-7eec-4188-9cf1-d2c205b72ac8" />


---

## 🛠️ How to Set It Up

1. Clone or import the workflow JSON (`workflow.json`) into your n8n instance.
2. Add your API credentials for: Telegram Bot Token, Gemini API key, and LinkedIn OAuth credentials.
3. Set up a LinkedIn Developer App to get your OAuth credentials — even if you're only posting to your *personal* profile, LinkedIn currently requires an associated Company Page to satisfy their app review requirements. You won't post to that page; it just needs to exist.
4. Update the following fields to match your setup:
   - Telegram `chat_id` → your own bot's chat ID
   - LinkedIn `person URN` → your personal profile's unique identifier (found via the LinkedIn API, not your profile URL)
5. Activate the workflow and test by sending yourself a sample idea via Telegram.

> ⚠️ Common mistakes I hit while building this:
> - **Wrong identifier:** LinkedIn's posting API needs your *person URN*, not your public profile URL — an easy early mix-up.
> - **OAuth scope errors:** if your LinkedIn app isn't requesting the exact right permission scopes, the post call fails silently or with a vague error — double-check your scopes match what the UGC endpoint requires.
> - **Stale `$json` references:** in n8n, once your data passes through an HTTP Request node, the `$json` context shifts to that node's output. Referencing an earlier node's data without pointing to it explicitly will quietly break your workflow.
> - **Static data not clearing between runs:** if you're testing repeatedly, leftover static data from a previous run can make you think a fix worked when it didn't. Clear it before every test.
> - **Dead-end node routing:** double-check every branch actually connects somewhere — a node with no downstream connection will just silently swallow your data.

---

## 📈 What I Learned / Why It Matters

- **Technical lesson:** Authenticating with a real platform's API (not just a no-code connector) teaches you things tutorials skip — like why context references break after certain node types, and why "it worked once" doesn't mean "it's reliable."
- **Business/strategic insight:** The bottleneck to consistent content was never *ideas* — it was the gap between having one and formatting it properly. Automating that gap is a repeatable pattern I can now offer as a service to any founder or consultant trying to build a personal brand.
- **Career/skill insight:** This project is a clean example of the "capture → AI-process → human-approve → publish" pattern, which shows up constantly in automation work — client intake forms, review responses, content pipelines. Once you've built it once, you start seeing it everywhere.

---

## 🙋🏽‍♀️ About This Project

Built by **Queen Ikwuji**, founder of **QueenEagleAI** — I help business owners and beginners automate repetitive work using AI agents, n8n, and no-code tools, and I teach what I build in public.

- 📌 Follow the build-in-public journey on [LinkedIn](www.linkedin.com/in/queen-ikwuji-8b925524a)
- 🎥 More automation breakdowns: [TiKTok link](https://www.tiktok.com/@queen.eagleai?_r=1&_t=ZS-97rM9NbIGJD)
- 💬 Want a custom workflow like this for your business? [Get in touch](queenikwuji@gmail.com)

---

*Got questions, ideas, or want to fork this for your own use case? Open an issue or reach out — I'd love to see what you build with it.*
