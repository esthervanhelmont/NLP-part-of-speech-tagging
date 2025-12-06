# Part-of-Speech Tagger Using a Hidden Markov Model (HMM)

This project builds a simple Part-of-Speech (POS) tagger that can automatically label words in a sentence with their grammatical category (such as NOUN, VERB, ADJ, etc.).  
The model is trained on the Brown Corpus using the Universal Tagset.  
The goal of the project is to understand how statistical sequence models work and to create an HMM from scratch.

---

## 1. What This Project Does

- We give the computer many example sentences where every word already has a correct tag.
- The computer studies these examples and learns:
  - **Which tags happen often** (e.g., NOUN appears the most)
  - **Which words belong to which tag** (e.g., “time” is usually a NOUN)
  - **Which tags follow each other** (e.g., DET is often followed by NOUN)
- We use these learned patterns to build a **Hidden Markov Model**.
- When we give the model a new sentence, it predicts the most likely tag for every word.

In short:  
**We teach the model how language works, and then it uses those rules to tag new sentences.**

---

## 2. Dataset Used

We train the model on a processed version of the **Brown Corpus**.

- The dataset contains **over 57,000 sentences**.
- Each sentence comes with correct POS tags.
- The Universal Tagset contains **12 tags** (e.g., NOUN, VERB, DET, ADJ, etc.).
- We split the data into:
  - **80% training**
  - **20% testing**

This gives the model enough examples to learn realistic language patterns.

---

## 3. Workflow of the Notebook

### Step 1 — Load and inspect the data  
We load the sentences, tags, and vocabulary. We check how many words and sentences we have.

### Step 2 — Count how often things happen  
To build an HMM, we need simple frequency tables:

- How often each tag appears (unigrams)  
- How often tag A is followed by tag B (bigrams)  
- How often a tag starts a sentence  
- How often a tag ends a sentence  
- How often a word appears with a tag (emissions)

These counts form the "knowledge" the model uses to understand grammar.

### Step 3 — Build a baseline model (Most-Frequent-Class Tagger)  
This simple model always picks the tag that a word had most often in the training data.

Example:  
If “run” is tagged as VERB 80% of the time and NOUN 20% of the time, the model always chooses VERB.

This gives a strong baseline and helps us compare whether the HMM does better.

### Step 4 — Build the Hidden Markov Model  
The HMM uses three types of probabilities:

1. **Start probabilities** How likely each tag is to begin a sentence  
2. **Transition probabilities** How likely one tag follows another  
3. **Emission probabilities** How likely each word is produced by each tag  

We create one state for each tag and connect them with the correct probabilities.

### Step 5 — Decode sentences using Viterbi  
The Viterbi algorithm finds the **most likely tag sequence** for a given sentence.

This allows the model to choose tags based not only on individual words but also based on context.

### Step 6 — Evaluate the model  
We compare predicted tags with the true tags.  
We measure accuracy on both:

- The training set  
- The testing set  

This tells us how well the model learned.

---

## 4. Results

- The **Most-Frequent-Class (MFC)** baseline performs strongly.
- The HMM further improves tagging by using **context**, not just individual words.
- The model correctly identifies common grammatical patterns, especially phrase structures like:
  - DET → NOUN  
  - PRON → VERB  
  - ADJ → NOUN

This shows that an HMM can capture real syntax patterns from data.

---

## 5. Why This Model Works

The HMM works because:

- Language has regular structure  
- Tags follow predictable patterns  
- Words are often tied to specific tags  
- Probabilities allow the model to choose the most realistic tag sequence  
