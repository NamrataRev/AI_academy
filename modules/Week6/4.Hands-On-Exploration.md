# Hands-on Exploration

---

## Learning Objectives

By the end of this topic, you should be able to:

- Describe what the TensorFlow Embedding Projector is and what it visualises
- Navigate the Embedding Projector tool to search for a word and inspect its nearest neighbours
- Identify clusters of semantically related words by observing their positions in the visualisation
- Explain why certain words appear close together and others appear far apart — connecting the visual result back to the cosine similarity maths you studied
- Evaluate the limitations of a 2D/3D visualisation of a high-dimensional embedding space

---

## Overview

You learned, by hand, exactly how embeddings and cosine similarity work. Now it's time to *see* real embeddings — not toy 2-number examples, but actual high-dimensional word embeddings, learned by a real model from real text — using a free, official visualisation tool built by Google's TensorFlow team: the **Embedding Projector**.

No coding is required. No installation. No login. Just a browser and careful observation.

Think of this like going from reading about how a city is laid out on a map, to actually flying over it and seeing the neighbourhoods, roads, and landmarks from above. The map was essential to understand the structure. But seeing it from above makes the pattern click in a way no map can.

The goal: build strong visual intuition for something you can currently only picture in your head — hundreds of words, positioned in space, clustering by meaning — so that when you study RAG and search later in this program, the underlying picture is already familiar and concrete, not abstract.

---

## What Is the Embedding Projector?

The **TensorFlow Embedding Projector** (available free at [projector.tensorflow.org](https://projector.tensorflow.org/)) is an official, browser-based visualisation tool. It takes real word embeddings — vectors with hundreds of dimensions, just like the mango and banana example you saw earlier — and **compresses** them down to just 2 or 3 dimensions you can actually see on screen.

Think of it like crushing a 3D object into a flat shadow on the floor. The shadow isn't a perfect copy — you lose some information — but it still shows you the overall shape and structure.

### Key Terms

| Term | Simple Meaning |
|---|---|
| **Projector** | The tool itself — projects high-dimensional data down to a viewable 2D or 3D space |
| **Nearest neighbours** | The words whose embeddings are closest (most similar by cosine similarity) to a chosen word |
| **Cluster** | A visible group of words sitting close together, suggesting they share related meaning |

---

## Guided Activity — Step by Step

Follow these steps in your browser. No installation, login, or coding required.

### Step 1 — Open the tool
Go to [projector.tensorflow.org](https://projector.tensorflow.org/) in your browser. You'll see a large 3D cloud of points — each point is one word's embedding, compressed for viewing.

### Step 2 — Search for "mango"
On the right-hand panel, find the search box. Type **"mango"** and click the word when it appears. The view zooms to that point and the right panel shows a ranked list of that word's **nearest neighbours** — the words with the most similar embeddings.

**Record what you observe:** What words appear as mango's nearest neighbours? You should expect to see other fruit names ranking highly.

### Step 3 — Search for "bicycle"
Now search for **"bicycle"** and note its nearest neighbours. Compare — does "bicycle" cluster anywhere near "mango"? It should not. The two words live in very different parts of the embedding space.

### Step 4 — Search for "bank"
Try the word **"bank"** — which has more than one common meaning (a riverbank vs a financial bank). Observe its neighbours. Do you see a mix of finance-related and geography-related words? This is a real, useful limitation of basic word embeddings: a single word gets only one embedding, blending all its senses together.

### Step 5 — Search for king, man, woman, queen
Search for **"king"**, **"man"**, **"woman"**, and **"queen"** individually, and visually compare their relative positions. While the 2D/3D compression won't let you verify the exact cosine similarity calculation by eye, you should notice these four words sitting in a related region of the space.

---

## Questions to Answer While Exploring

As you explore the tool, these questions will help you connect what you see visually to the mathematics you already understand. Write down your observations — you will need them for reflection.

- Which words clustered tightly around "mango"? Were they what you expected?
- Was there any surprising or confusing neighbour in any of your searches? What might explain it?
- For the word "bank" — could this ambiguity cause a real AI system, like a customer-support chatbot for a bank, to make a mistake? How?
- After seeing the clusters visually, does the cosine similarity calculation you did by hand make more intuitive sense now?

---

## Important Limitations to Know

**The visualisation is a compression, not the real thing.** The actual embedding has 100+ dimensions. The picture you see has been squeezed into 2 or 3. Two words can look reasonably close in the picture but be less similar than they appear — or vice versa. Treat the visualisation as a helpful *intuition tool*, not a mathematically exact reading.

In real systems, always trust the actual computed cosine similarity score over a visual impression alone.

**This tool uses a general-purpose embedding model** trained on generic text — not Claude's internal representations. It is used here purely to build visual intuition about how any embedding space behaves.

---

## Worked Example — Searching for "dollar"

**What to search:** Type "dollar" in the Embedding Projector.

**Expected observation:** Nearest neighbours likely include other currency-related words — "euro," "currency," "money," "price," "pound" — because the model learned these words appear in similar contexts across huge volumes of real text such as news articles discussing prices, exchange rates, and global finance.

**Connecting back to the maths:** Each of these words has its own high-dimensional embedding vector. The reason "dollar" and "euro" cluster together is that their vectors have a **high cosine similarity** — precisely the calculation you performed by hand earlier, just now happening automatically across hundreds of dimensions, for every pair of words in the entire vocabulary.

**The full picture:** This single exploration ties together the whole unit:

- Everything is numbers → organised as vectors → compared using cosine similarity → visualised as real, observable clusters

This is the mental model you will rely on throughout the rest of this program — every time you encounter search, RAG, or recommendation systems.

---

## Key Takeaways

- The **TensorFlow Embedding Projector** is a free, official tool for visualising real high-dimensional word embeddings, compressed to 2D or 3D
- Searching a word shows its **nearest neighbours** — the words with the most similar embeddings (highest cosine similarity)
- Semantically related words form visible **clusters** — unrelated words sit far apart
- Ambiguous words like "bank" reveal a real limitation: one embedding may blend multiple meanings into one point
- The visualisation is a **compressed approximation** — always trust the actual computed similarity score over visual impression alone
- This hands-on exploration is the visual counterpart to the hand-calculated maths — the same underlying principle (closeness = similarity) at real-world scale

> **Interview tip:** Being able to explain *why* two words cluster together — in terms of cosine similarity of their embeddings — is a strong, concrete way to demonstrate you understand embeddings beyond buzzwords. "They cluster because their embedding vectors have a high cosine similarity, meaning they appeared in similar contexts during training" is the precise, correct answer.

---

## Reference Links

- 📎 [TensorFlow Embedding Projector](https://projector.tensorflow.org/) — the official tool used in this activity
- 📎 [TensorFlow Documentation — Word Embeddings](https://www.tensorflow.org/text/guide/word_embeddings) — official background reading on how embeddings are learned
- 📎 [Google ML Crash Course — Embeddings](https://developers.google.com/machine-learning/crash-course) — supplementary conceptual grounding
