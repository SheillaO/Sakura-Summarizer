# 🌸 Sakura Summarizer

*A hands-on exploration of the Hugging Face Inference API — by Sheilla Olga | [GitHub](https://github.com/SheillaO) · [LinkedIn](https://linkedin.com/in/sheillaolga)*

---

## What this is

A small, deliberately-scoped script that sends a 200-word passage about Japan's cherry blossom season to a Hugging Face-hosted summarization model and gets back a tight, two-sentence summary.

It's not trying to be impressive on size. It's the first committed piece of a learning-in-public series on practical AI engineering — the kind of hands-on, model-level understanding I think every technical PMM should have before they write a single word of positioning for an AI feature.

## Why I built this

I spent years on the partnerships side of tech translating platform capability into deals and go-to-market decisions. I'm now building toward Technical Product Marketing — and I don't think you can credibly market AI products without having actually sat inside the API calls, watched the latency, and felt where a model's outputs get weird.

This repo is where I do that sitting-inside-it work, one small, real, shippable piece at a time.

## At a glance

|  |  |
| --- | --- |
| **Task** | Text summarization |
| **Model** | `facebook/bart-large-cnn` |
| **Provider** | Hugging Face Inference API |
| **Input** | \~200-word source passage |
| **Output** | 2–3 sentence abstractive summary |
| **Runtime** | Node.js |

## How it works

```js
import { InferenceClient } from "@huggingface/inference";
const client = new InferenceClient(process.env.HF_TOKEN);

export async function textSummarization() {
  const response = await client.summarization({
    model: "facebook/bart-large-cnn",
    inputs: inputText,
    provider: "hf-inference",
  });

  return response;
}
```

The `InferenceClient` abstracts away the raw HTTP layer, so the interesting decision isn't *how* to call the API — it's *which model* to call it with. More on that below.

## Quick start

```bash
npm install @huggingface/inference
export HF_TOKEN=your_token_here
node index.js
```

## The product lens

Here's the part I actually find interesting, and the reason this repo exists rather than just living in a throwaway sandbox:

`facebook/bart-large-cnn` isn't a general-purpose chat model doing summarization as one trick among many — it's a model *fine-tuned specifically* on the CNN/DailyMail news dataset, purpose-built for exactly one job. That's a deliberate product trade-off, not a technical detail:

- **A fine-tuned, single-task model** (like BART-CNN here) tends to be faster, cheaper, and more consistent for that one job — but it's inflexible outside of it.
- **A general-purpose generative model** can summarize *and* chat *and* translate *and* reason — but you pay for that flexibility in latency, cost, and sometimes unpredictability.

That's the exact kind of trade-off a PMM has to understand to write an honest feature announcement, brief a sales team, or push back on an engineering roadmap that's reaching for the flashiest model instead of the right-sized one. You can't make that call from a slide deck — you have to have run both kinds of models and felt the difference.

## What's next

This repo is intentionally built to grow rather than stay a single script. Next up, as I work through the rest of the curriculum:

- [ ] **Image tasks** — captioning and classification via Hugging Face's vision models
- [ ] **Transformers deep dive** — understanding what's actually happening inside the models I'm calling, not just calling them
- [ ] **A lightweight chat interface** — early scaffolding for this already exists in the repo and is actively being wired up

Each addition will get its own section here, so this README functions less like a one-off project writeup and more like a running log of what I've actually built and understood.

## A note on scope

This is one script. I'm not going to pretend it's more than that. What it represents — a deliberate habit of building and documenting real, working AI integrations rather than only reading about them — is the thing I'd actually want a recruiter or hiring manager to notice.

---

*Part of my [TPMM portfolio](https://github.com/SheillaO) — built on Scrimba's AI Engineering curriculum.*