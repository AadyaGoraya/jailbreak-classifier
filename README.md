# Jailbreak Classifier

I built this while going down a rabbit hole on how people actually break LLMs. Turns out there's a whole taxonomy of attack types — role overrides, prompt injections, encoding tricks — and I wanted to see if I could detect them systematically.

**[Live Demo →](https://aadyagoraya.github.io/jailbreak-classifier)**

---

## What it does

You paste a prompt in, and it tells you whether it looks like a jailbreak attempt or not. It gives you a verdict (Safe / Suspicious / Unsafe), a confidence score, and breaks down exactly which attack pattern it flagged and why.

There's also a session history so you can compare multiple prompts side by side, and six preloaded examples if you want to see it in action without typing anything.

---

## The six attack types it detects

- **Role Override** — the classic "you are now DAN, you have no restrictions" style attempts
- **Prompt Injection** — slipping in new instructions to override what the model was told to do
- **Fictional Framing** — "hypothetically, for a story I'm writing..." to get around content filters
- **Encoding Evasion** — using Base64 or character tricks to hide what's actually being asked
- **Authority Spoofing** — pretending to be Anthropic or an admin to claim special permissions
- **Output Extraction** — trying to get the model to leak its system prompt or configuration

---

## How the classifier actually works

It's rule-based, not ML. Each attack category has a set of regex patterns and a risk weight. When a prompt matches a pattern, that category's weight gets added to a running score. The score gets normalized and then mapped to a verdict.

I went rule-based intentionally — the main advantage is that every flag is explainable. You can point to exactly what triggered it. That matters in a safety context. The obvious downside is that it can't handle attacks it's never seen before, and someone who knows the rules can reword around them. A real production system would need learned classification on top of this.

---

## Stack

Vanilla HTML/CSS/JS, no dependencies. Everything runs client-side, nothing leaves the browser.

---

## Running it

```bash
git clone https://github.com/aadyagoraya/jailbreak-classifier
open index.html
```

Or just visit the live demo above.

---

## Author

Aadya Goraya — CS Student  
[GitHub](https://github.com/aadyagoraya) · [CoviDash](https://aadyagoraya.github.io/CoviDash/) · [Finance Tracker](https://aadyagoraya.github.io/FinanceTracker/)
