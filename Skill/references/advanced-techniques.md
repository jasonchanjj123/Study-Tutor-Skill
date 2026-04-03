# Advanced Study Techniques Reference

This file contains additional study method templates and cognitive science principles. Consult this when building study materials for advanced students, graduate-level courses, or when the user specifically requests deeper learning techniques.

## Table of Contents
1. Spaced Repetition Scheduling
2. Elaborative Interrogation
3. Interleaving Practice
4. Dual Coding Theory
5. Method of Loci (Memory Palace)
6. Cornell Note Method Restructuring
7. Bloom's Taxonomy Question Design
8. SQ3R Reading Framework
9. Pomodoro-Aligned Study Sessions

---

## 1. Spaced Repetition Scheduling

When generating flashcards, you can optionally tag them with a suggested review schedule based on the Ebbinghaus forgetting curve:

- **Session 1** (today): All new cards
- **Session 2** (tomorrow): Cards missed + random 30% of cards passed
- **Session 3** (day 3): All previously missed + random 20%
- **Session 4** (day 7): Full review
- **Session 5** (day 14): Full review
- **Session 6** (day 30): Final review

In the HTML, you can add a "Study Plan" section that maps this schedule with actual dates based on the student's exam date (if provided).

## 2. Elaborative Interrogation

For each key claim or fact in the material, generate a "Why?" question. This forces the student to explain the mechanism, not just memorize the outcome.

Template:
```
FACT: [Statement from the notes]
WHY QUESTION: Why is this the case? / Why does this work this way?
DEEP ANSWER: [Explanation of the underlying mechanism]
WHAT IF: What would change if [variable] were different?
```

Use this technique especially for science, engineering, and economics material where cause-and-effect chains are central.

## 3. Interleaving Practice

Instead of grouping all similar problems together ("blocked practice"), mix problems from different topics in the exercise section. Research shows interleaving improves long-term retention and discrimination between problem types.

When building exercises:
- After every 3 questions on Topic A, insert 1 question on a previously covered topic
- In the Synthesis tier, always mix concepts from different sections
- Label interleaved questions with the source topic so students can trace back if confused

## 4. Dual Coding Theory

Wherever possible, represent information in both verbal and visual form. The brain processes these through separate channels, creating redundant memory traces.

Strategies:
- Every formula should have both the symbolic version and a diagram/visual showing what each variable represents physically
- Every process should have both a prose description and a flowchart/diagram
- Every comparison should have both a written explanation and a table or Venn diagram
- For code: include both the code block and a visual trace/diagram of execution

In the HTML, use side-by-side layouts: text on left, visual on right.

## 5. Method of Loci (Memory Palace)

For courses with many items to memorize in sequence (e.g., historical events, biological processes, protocol steps), offer a "Memory Palace" walkthrough:

1. Choose a familiar physical space (e.g., the student's apartment)
2. Assign each item to a location in the space, in order
3. Create a vivid, absurd mental image linking the item to the location
4. Walk through the space mentally to recall the sequence

In the study guide, include a template section:
```
🏠 Memory Palace: [Topic Name]
Room 1 (Front Door): [Item 1] — Imagine [vivid image suggestion]
Room 2 (Living Room): [Item 2] — Imagine [vivid image suggestion]
...
```

This is optional and best for list-heavy material. Ask the student if they want this.

## 6. Cornell Note Restructuring

If the student's original notes are messy or stream-of-consciousness, restructure them into Cornell format:

| Cue Column (left 30%) | Notes Column (right 70%) |
|----------------------|------------------------|
| Key question or keyword | Detailed notes, examples, diagrams |
| | |
| **Summary (bottom)** | 2-3 sentence summary of the entire page |

This is a reorganization technique — don't use it for the final study guide output (the HTML format is better), but mention it as a suggested note-taking improvement for future lectures.

## 7. Bloom's Taxonomy Question Design

Map exercise questions to Bloom's cognitive levels to ensure comprehensive coverage:

| Level | Verbs | Example Stem |
|-------|-------|-------------|
| Remember | List, Define, Recall | "What are the three types of..." |
| Understand | Explain, Summarize, Paraphrase | "In your own words, describe..." |
| Apply | Solve, Use, Implement | "Given this scenario, calculate..." |
| Analyze | Compare, Differentiate, Examine | "What are the key differences between..." |
| Evaluate | Justify, Critique, Assess | "Which approach is better for X and why?" |
| Create | Design, Construct, Propose | "Design a system that..." |

The Tier 1/2/3 structure in the main skill roughly maps to Remember+Understand / Apply+Analyze / Evaluate+Create. Use these verbs to sharpen your question phrasing.

## 8. SQ3R Reading Framework

When summarizing textbook-heavy material, structure the study guide using SQ3R:

- **Survey**: Quick overview of what the chapter covers (table of contents, learning objectives)
- **Question**: Convert each heading into a question the student should be able to answer after studying
- **Read**: The detailed summary content
- **Recite**: Flashcards and self-test questions
- **Review**: The quick-reference cheat sheet and connections to other material

This gives the study guide a natural flow that mirrors effective reading strategy.

## 9. Pomodoro-Aligned Study Sessions

For very large study guides, add a suggested study schedule that breaks the material into 25-minute focused sessions:

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

This is helpful when the student says they have limited time or asks "how should I study this?"
