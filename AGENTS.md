# PROJECT KNOWLEDGE BASE

**Course:** Formalising Mathematics
**Code:** MATH70063
**Term:** Spring 2025

## OVERVIEW

Imperial College MSc course notes for Formalising Mathematics. The main Lean 4 codebase for this course is maintained in a separate external project.

## STRUCTURE

```
FormalisingMathematics/
├── Notes/
│   ├── main.tex          # Main lecture notes
│   ├── preamble.sty      # Shared style
│   ├── chapters/         # Chapter files
│   └── figures/          # Diagrams
├── README.md             # Link to external Lean project
└── AGENTS.md            # This file
```

## LECTURER

- **Name**: Kevin Buzzard
- **Office Hours**: TBD

## EXTERNAL LEAN PROJECT

The core Lean 4 formalisations for this course are maintained separately:

**Location**: [TBD - Insert path or GitHub link]

This repository contains the mathematical context and lecture notes that accompany the Lean formalisation work.

## SYLLABUS

TBD - Add topics as course progresses

## CONVENTIONS

- Theorem environments: theorem, lemma, proposition, corollary, definition, example, remark
- References: Use `\cref{}` (cleveref)
- Diagrams: tikz-cd for commutative diagrams
- Lean references: Note file names and line numbers linking to external codebase

## COMMANDS

```bash
# Compile notes
cd Notes && latexmk -pdf main.tex
```

## RESOURCES

- [Formalising Mathematics in Lean](https://www.ma.imperial.ac.uk/~buzzard/xena/formalising-mathematics-2024/)
- External Lean Project: [TBD]
