# Advanced Study Techniques Reference

This file contains study method templates, cognitive science principles, and HTML implementation patterns. Consult this when building study materials for advanced students, graduate-level courses, or when the user specifically requests deeper learning techniques.

## Table of Contents
1. Spaced Repetition Scheduling (with interactive calendar)
2. Elaborative Interrogation
3. Interleaving Practice
4. Dual Coding Theory (with implementation patterns)
5. Method of Loci (Memory Palace)
6. Cornell Note Method Restructuring
7. Bloom's Taxonomy Question Design
8. SQ3R Reading Framework
9. Pomodoro-Aligned Study Sessions
10. Retrieval Practice Ladders
11. Concept Dependency Sequencing
12. Self-Explanation Protocol
13. Worked Example → Fading Strategy
14. Diagnostic Pre-Test
15. Metacognitive Confidence Calibration
16. Comparison Matrix Builder

---

## 1. Spaced Repetition Scheduling

When generating flashcards, tag them with a review schedule based on the Ebbinghaus forgetting curve:

- **Session 1** (today): All new cards
- **Session 2** (tomorrow): Cards missed + random 30% of cards passed
- **Session 3** (day 3): All previously missed + random 20%
- **Session 4** (day 7): Full review
- **Session 5** (day 14): Full review
- **Session 6** (day 30): Final review

### Interactive Calendar Implementation

When the student provides an exam date, generate an interactive calendar in the study guide:

```javascript
function generateSpacedSchedule(examDateStr) {
  const exam = new Date(examDateStr);
  const intervals = [0, 1, 3, 7, 14, 30];
  const sessions = intervals
    .map(days => {
      const d = new Date(exam);
      d.setDate(d.getDate() - days);
      return d;
    })
    .filter(d => d >= new Date())
    .sort((a, b) => a - b);

  return sessions.map((date, i) => ({
    date: date.toLocaleDateString('en-US', { weekday: 'short', month: 'short', day: 'numeric' }),
    label: i === sessions.length - 1 ? '🎯 Exam Day' : `Session ${i + 1}`,
    focus: i === 0 ? 'First pass: all cards' :
           i < 3 ? 'Review missed + random sample' : 'Full review'
  }));
}
```

Render as a visual timeline in Section G (Study Planner).

---

## 2. Elaborative Interrogation

For each key claim or fact, generate a "Why?" question forcing the student to explain the mechanism.

Template:
```
FACT: [Statement from the notes]
WHY QUESTION: Why is this the case? / Why does this work this way?
DEEP ANSWER: [Explanation of the underlying mechanism]
WHAT IF: What would change if [variable] were different?
```

Use especially for science, engineering, and economics where cause-and-effect chains are central.

---

## 3. Interleaving Practice

Mix problems from different topics instead of grouping similar ones ("blocked practice"). Research shows interleaving improves long-term retention.

When building exercises:
- After every 3 questions on Topic A, insert 1 question on a previously covered topic
- In the Synthesis tier, always mix concepts from different sections
- Label interleaved questions with the source topic so students can trace back

### Implementation
Add a small colored badge to interleaved questions:

```html
<span class="interleave-tag" style="
  background: #ffe0b2; color: #e65100;
  padding: 2px 8px; border-radius: 12px;
  font-size: 11px; margin-left: 8px;
">↩ from: Topic A</span>
```

---

## 4. Dual Coding Theory

Represent information in both verbal and visual form — the brain processes these through separate channels, creating redundant memory traces.

Strategies:
- Every formula: symbolic version + annotated diagram showing what each variable represents
- Every process: prose description + flowchart/diagram
- Every comparison: written explanation + table or Venn diagram
- For code: code block + visual execution trace

### Side-by-Side Layout

```html
<div class="dual-code" style="display:grid; grid-template-columns:1fr 1fr; gap:24px; align-items:start;">
  <div class="verbal">
    <h4>Explanation</h4>
    <p>The gradient points in the direction of steepest ascent...</p>
  </div>
  <div class="visual">
    <h4>Visual</h4>
    <!-- SVG diagram or annotated formula here -->
  </div>
</div>
```

### Formula Annotation Pattern

For math/science courses, annotate formulas with a variable legend rendered in KaTeX:

```html
<div class="annotated-formula">
  \[ F = ma \]
  <table class="formula-legend" style="font-size:13px; margin:8px auto;">
    <tr><td>\( F \)</td><td>— Net force (Newtons)</td></tr>
    <tr><td>\( m \)</td><td>— Mass of the object (kg)</td></tr>
    <tr><td>\( a \)</td><td>— Acceleration (m/s²)</td></tr>
  </table>
</div>
```

---

## 5. Method of Loci (Memory Palace)

For courses with many sequential items to memorize (historical events, biological processes, protocol steps):

1. Choose a familiar physical space
2. Assign each item to a location in the space, in order
3. Create a vivid, absurd mental image linking the item to the location
4. Walk through the space mentally to recall the sequence

Template:
```
🏠 Memory Palace: [Topic Name]
Room 1 (Front Door): [Item 1] — Imagine [vivid image suggestion]
Room 2 (Living Room): [Item 2] — Imagine [vivid image suggestion]
```

Optional — best for list-heavy material (>7 sequential items).

---

## 6. Cornell Note Restructuring

If the student's original notes are messy, restructure into Cornell format:

| Cue Column (left 30%) | Notes Column (right 70%) |
|----------------------|------------------------|
| Key question or keyword | Detailed notes, examples, diagrams |
| **Summary (bottom)** | 2-3 sentence summary of the entire page |

Don't use for final study guide output (HTML format is better), but mention it as a note-taking improvement for future lectures.

---

## 7. Bloom's Taxonomy Question Design

Map exercise questions to Bloom's cognitive levels:

| Level | Verbs | Example Stem |
|-------|-------|-------------|
| Remember | List, Define, Recall | "What are the three types of..." |
| Understand | Explain, Summarize, Paraphrase | "In your own words, describe..." |
| Apply | Solve, Use, Implement | "Given this scenario, calculate..." |
| Analyze | Compare, Differentiate, Examine | "What are the key differences between..." |
| Evaluate | Justify, Critique, Assess | "Which approach is better for X and why?" |
| Create | Design, Construct, Propose | "Design a system that..." |

The Tier 1/2/3 structure maps to Remember+Understand / Apply+Analyze / Evaluate+Create.

---

## 8. SQ3R Reading Framework

Structure textbook-heavy study guides using SQ3R:

- **Survey**: Quick overview (table of contents, learning objectives)
- **Question**: Convert each heading into a question the student should answer after studying
- **Read**: Detailed summary content
- **Recite**: Flashcards and self-test questions
- **Review**: Quick-reference cheat sheet and connections to other material

---

## 9. Pomodoro-Aligned Study Sessions

Break large study guides into 25-minute focused sessions:

```
📅 Suggested Study Plan (estimated X hours total)
Session 1 (25 min): Read Chapter Summary Sections A-C
  🍅 Break (5 min)
Session 2 (25 min): Flashcard deck — first pass (all cards)
  🍅 Break (5 min)
Session 3 (25 min): Feynman explanations — read and re-explain in your own words
  🍅 Break (5 min)
Session 4 (25 min): Tier 1 & 2 exercises
  🍅 Long break (15 min)
Session 5 (25 min): Tier 3 exercises + Knowledge graph review
Session 6 (25 min): Flashcard deck — second pass (missed cards only)
```

---

## 10. Retrieval Practice Ladders

Build a progressive difficulty chain for each core concept. 4 rungs per concept:

| Rung | Type | Example |
|------|------|---------|
| 1. Recognition | Multiple choice / true-false | "Which of these is the formula for..." |
| 2. Cued recall | Fill-in-the-blank with context | "The time complexity of binary search is ___" |
| 3. Free recall | Open-ended, no cues | "Explain how binary search works and its complexity" |
| 4. Transfer | Apply to novel situation | "You have 1M sorted items on disk with slow random access. Is binary search ideal? Why?" |

### When to use
- 3-6 critical concepts the student *must* master
- Student says "I need to really nail this topic"
- Exam mixes recognition and free-recall

### Implementation
Build each ladder as a collapsible section — student reveals each rung only after attempting the previous one:

```html
<div class="retrieval-ladder">
  <h4>🪜 Retrieval Ladder: Binary Search</h4>
  <div class="rung" id="rung-1">
    <p class="rung-label">Rung 1 — Recognition</p>
    <p>Which is the time complexity of binary search? A) O(n) B) O(log n) C) O(n log n) D) O(1)</p>
    <button onclick="document.getElementById('rung-1-answer').style.display='block'">Check</button>
    <div id="rung-1-answer" style="display:none">
      <p>✅ B) O(log n)</p>
      <button onclick="document.getElementById('rung-2').style.display='block'">Next Rung →</button>
    </div>
  </div>
  <div class="rung" id="rung-2" style="display:none"><!-- ... --></div>
</div>
```

---

## 11. Concept Dependency Sequencing

Before building Section A (Chapter Summary), analyze the dependency graph and reorder by **topological sort** — prerequisites first, dependent concepts after.

**Algorithm:**
1. List all concepts from the content inventory
2. For each, identify which other concepts it depends on
3. Order so no concept appears before its prerequisites
4. Group into "levels" — Level 0 has no prerequisites, Level 1 depends only on Level 0, etc.

This ensures the student never encounters an unexplained term. Flag circular dependencies — these need a "bootstrap" explanation introducing both concepts at a high level first.

The dependency levels can also map to vertical position in the Knowledge Graph (Section D).

---

## 12. Self-Explanation Protocol

After each worked example or solved problem, prompt the student to self-explain. Research (Chi et al., 1989) shows students who explain each step learn 2-3x more.

**Add after every "Show Answer" block:**

```html
<div class="self-explain-prompt" style="
  background: #e3f2fd; border-left: 4px solid #1976d2;
  padding: 12px 16px; margin-top: 12px; border-radius: 0 8px 8px 0;
">
  <p style="margin:0; font-weight:600;">🧠 Self-Explain Check</p>
  <p style="margin:4px 0 0;">Can you explain <em>why</em> each step follows from the previous one? If any step feels like a magic leap, that's where to focus review.</p>
</div>
```

---

## 13. Worked Example → Fading Strategy

For problem-heavy courses (math, physics, CS algorithms), use a 4-step fading sequence:

1. **Full worked example** — every step shown and explained
2. **Partially worked** — some steps shown, student fills blanks
3. **Scaffolded** — only setup and final answer given
4. **Independent** — just the problem, no help

### Implementation — 4-tab interface per key problem type:

```html
<div class="fading-tabs">
  <button class="tab active" onclick="showTab(this,'full')">Full Example</button>
  <button class="tab" onclick="showTab(this,'partial')">Fill the Gaps</button>
  <button class="tab" onclick="showTab(this,'scaffold')">Guided</button>
  <button class="tab" onclick="showTab(this,'independent')">On Your Own</button>
  <div id="full" class="tab-content"><!-- Complete solution --></div>
  <div id="partial" class="tab-content" style="display:none"><!-- Steps 2,4 blanked --></div>
  <div id="scaffold" class="tab-content" style="display:none"><!-- Given/Find + answer only --></div>
  <div id="independent" class="tab-content" style="display:none"><!-- Problem statement only --></div>
</div>
```

Use for the 2-3 most representative problem types per chapter. Especially valuable for math/science procedural fluency.

---

## 14. Diagnostic Pre-Test

Add an optional "How much do you already know?" section at the very top of the study guide:

- 5-8 quick questions (mix of easy and hard)
- Immediate feedback after each
- Summary at end: "You seem solid on X and Y. Focus on Z."

**Purpose:** Activates prior knowledge (priming effect) and identifies weak spots before reading.

Track correct/incorrect via JS and generate a personalized focus recommendation.

---

## 15. Metacognitive Confidence Calibration

After each exercise question, before revealing the answer, ask:

```
How confident are you? 😟 Guessing | 🤔 Somewhat sure | 😊 Very confident
```

After reveal, show calibration feedback:
- **Confident + Correct** → "Nice! Well calibrated."
- **Confident + Wrong** → "⚠️ Dangerous blind spot — you thought you knew this. Flag for extra review."
- **Guessing + Correct** → "Lucky or intuition? Try to articulate *why* this is correct."
- **Guessing + Wrong** → "Expected — add to your priority review list."

Research on metacognition shows that knowing *what you don't know* is half the battle. Add confidence buttons before each "Show Answer" and track calibration stats.

---

## 16. Comparison Matrix Builder

For material with multiple similar concepts students confuse (TCP vs UDP, mitosis vs meiosis, sorting algorithms), build an interactive comparison matrix.

### Interactive version — cells hidden, student clicks to reveal:

```html
<table class="comparison-matrix">
  <tr><th></th><th>TCP</th><th>UDP</th></tr>
  <tr>
    <td>Connection</td>
    <td class="hidden-cell" onclick="this.classList.toggle('revealed')">
      <span class="cell-hidden">Click to reveal</span>
      <span class="cell-content">Connection-oriented (3-way handshake)</span>
    </td>
    <td class="hidden-cell" onclick="this.classList.toggle('revealed')">
      <span class="cell-hidden">Click to reveal</span>
      <span class="cell-content">Connectionless</span>
    </td>
  </tr>
</table>
<style>
  .hidden-cell .cell-content { display: none; }
  .hidden-cell .cell-hidden { color: #999; cursor: pointer; font-style: italic; }
  .hidden-cell.revealed .cell-content { display: inline; }
  .hidden-cell.revealed .cell-hidden { display: none; }
</style>
```

Use when 3+ concepts share a category but differ in key ways.

---

## Choosing Techniques by Course Type

| Technique | STEM/Math | Programming | Humanities | Business |
|-----------|-----------|-------------|------------|----------|
| Spaced Repetition | ✅ | ✅ | ✅ | ✅ |
| Elaborative Interrogation | ✅✅ | ✅ | ✅✅ | ✅ |
| Interleaving | ✅✅ | ✅ | ✅ | ✅ |
| Dual Coding | ✅✅ | ✅✅ | ✅ | ✅✅ |
| Memory Palace | ✅ | ⬜ | ✅✅ | ⬜ |
| Retrieval Ladders | ✅✅ | ✅✅ | ✅ | ✅ |
| Worked Example Fading | ✅✅ | ✅✅ | ⬜ | ✅ |
| Diagnostic Pre-Test | ✅ | ✅ | ✅ | ✅ |
| Confidence Calibration | ✅✅ | ✅ | ✅ | ✅ |
| Comparison Matrix | ✅ | ✅✅ | ✅✅ | ✅✅ |

✅✅ = highly recommended · ✅ = useful · ⬜ = rarely needed
