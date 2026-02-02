# Plan: Add Subfiles Support for Chapter-Level Compilation

## Goal
Enable independent compilation of each chapter file while maintaining full preamble/reference support.

---

## Tasks

### Task 1: Add `subfiles` package to preamble
**File**: `Notes/preamble.sty`  
**Action**: Add after line 18 (after cleveref)

```tex
% Subfiles for chapter-level compilation
\RequirePackage{subfiles}
```

### Task 2: Convert `ch01-introduction.tex` to subfiles format
**File**: `Notes/chapters/ch01-introduction.tex`  
**Action**: Replace entire content with:

```tex
\documentclass[../main.tex]{subfiles}
\begin{document}

\section{Introduction}

Notes will be added here.

\end{document}
```

### Task 3: Convert `ch02-type-theory-of-lean.tex` to subfiles format
**File**: `Notes/chapters/ch02-type-theory-of-lean.tex`  
**Action**: Replace entire content with:

```tex
\documentclass[../main.tex]{subfiles}
\begin{document}

\section{Type Theory of Lean}

Notes will be added here.

\end{document}
```

### Task 4: Clean up and update .gitignore
**Actions**:
1. Delete backup files:
   - `Notes/chapters/ch01-introduction.bak0`
   - `Notes/chapters/ch02-type-theory-of-lean.bak0`
   - `Notes/main.bak1`
   - `Notes/main.bak2`

2. Add to `.gitignore` (create if not exists):
```
# LaTeX build artifacts
*.bak*
Notes/out/
Notes/main.pdf
```

### Task 5: Git commit and push
**Commands**:
```bash
git add -A
git commit -m "feat(latex): add subfiles support for chapter-level compilation"
git push
```

---

## Verification
After execution, test by:
```bash
cd Notes/chapters && pdflatex ch02-type-theory-of-lean.tex
```
Should compile independently without errors.

---

## Summary
- **Files modified**: 3 (preamble.sty, ch01, ch02)
- **Files deleted**: 4 (.bak files)
- **Files created/updated**: 1 (.gitignore)
- **Commits**: 1
- **Pushes**: 1
