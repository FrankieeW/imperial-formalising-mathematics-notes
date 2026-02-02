# Plan: Add Evan Chen Colorful Theorem Boxes

## Goal
Replace current plain theorem environments with Evan Chen's colorful theorem boxes using mdframed + tcolorbox.

---

## Prerequisites Check

Before starting, verify LaTeX packages are installed:
```bash
kpsewhich mdframed.sty
kpsewhich thmtools.sty
kpsewhich tcolorbox.sty
```

If missing, install via:
```bash
tlmgr install mdframed thmtools tcolorbox
```

---

## Tasks

### Task 1: Backup current preamble
**File**: `Notes/preamble.sty`  
**Action**: Create backup
```bash
cp Notes/preamble.sty Notes/preamble.sty.backup-$(date +%Y%m%d-%H%M%S)
```

### Task 2: Add required packages to preamble
**File**: `Notes/preamble.sty`  
**Location**: After line 5 (after xcolor)  
**Add**:
```tex
% Colorful theorem boxes (Evan Chen style)
\RequirePackage[framemethod=TikZ]{mdframed}
\RequirePackage{thmtools}
\RequirePackage{tcolorbox}
\tcbuselibrary{theorems,skins,breakable}
```

### Task 3: Define color palette
**File**: `Notes/preamble.sty`  
**Location**: After the new package imports  
**Add**:
```tex
% Color definitions for theorem boxes
\definecolor{TealBlue}{RGB}{0,128,128}
\definecolor{Salmon}{RGB}{250,128,114}
\definecolor{ForestGreen}{RGB}{34,139,34}
\definecolor{RawSienna}{RGB}{199,97,20}
\definecolor{RedViolet}{RGB}{199,21,133}
```

### Task 4: Define mdframed styles
**File**: `Notes/preamble.sty`  
**Location**: Before theorem environment definitions  
**Add**:
```tex
% Blue box style (for theorems, lemmas, propositions, corollaries)
\mdfdefinestyle{mdbluebox}{%
    roundcorner=10pt,
    linewidth=1pt,
    skipabove=12pt,
    innerbottommargin=9pt,
    skipbelow=2pt,
    linecolor=TealBlue,
    nobreak=true,
    backgroundcolor=TealBlue!5,
}

% Red box style (for examples)
\mdfdefinestyle{mdredbox}{%
    roundcorner=10pt,
    linewidth=1pt,
    skipabove=12pt,
    innerbottommargin=9pt,
    skipbelow=2pt,
    linecolor=RawSienna,
    nobreak=true,
    backgroundcolor=Salmon!5,
}

% Green box style (for algorithms, claims)
\mdfdefinestyle{mdgreenbox}{%
    skipabove=8pt,
    linewidth=2pt,
    rightline=false,
    leftline=true,
    topline=false,
    bottomline=false,
    linecolor=ForestGreen,
    backgroundcolor=ForestGreen!5,
}

% Black box style (for remarks, notes)
\mdfdefinestyle{mdblackbox}{%
    skipabove=8pt,
    linewidth=2pt,
    rightline=false,
    leftline=true,
    topline=false,
    bottomline=false,
    linecolor=black,
    backgroundcolor=RedViolet!5!gray!5,
}
```

### Task 5: Replace theorem environment definitions
**File**: `Notes/preamble.sty`  
**Replace**: Current theorem definitions (lines ~22-31)  
**With**:
```tex
% Theorem environments with colorful boxes
\declaretheoremstyle[
    headfont=\sffamily\bfseries\color{TealBlue},
    mdframed={style=mdbluebox},
    headpunct={\\[3pt]},
    postheadspace={0pt}
]{thmbluebox}

\declaretheoremstyle[
    headfont=\sffamily\bfseries\color{RawSienna},
    mdframed={style=mdredbox},
    headpunct={\\[3pt]},
    postheadspace={0pt}
]{thmredbox}

\declaretheoremstyle[
    headfont=\sffamily\bfseries\color{ForestGreen},
    mdframed={style=mdgreenbox},
    headpunct={\\[3pt]},
    postheadspace={0pt}
]{thmgreenbox}

\declaretheoremstyle[
    headfont=\sffamily\bfseries,
    mdframed={style=mdblackbox},
    headpunct={\\[3pt]},
    postheadspace={0pt}
]{thmblackbox}

% Define theorem-like environments
\declaretheorem[style=thmbluebox, name=Theorem, numberwithin=section]{theorem}
\declaretheorem[style=thmbluebox, name=Lemma, sibling=theorem]{lemma}
\declaretheorem[style=thmbluebox, name=Proposition, sibling=theorem]{proposition}
\declaretheorem[style=thmbluebox, name=Corollary, sibling=theorem]{corollary}

% Definition environment (blue box, unnumbered style also available)
\declaretheorem[style=thmbluebox, name=Definition, sibling=theorem]{definition}

% Example environment (red box)
\declaretheorem[style=thmredbox, name=Example, numberwithin=section]{example}

% Exercise environment (red box)
\declaretheorem[style=thmredbox, name=Exercise, numberwithin=section]{exercise}

% Remark environment (black box)
\declaretheorem[style=thmblackbox, name=Remark, numberwithin=section]{remark}

% Notation environment (green box)
\declaretheorem[style=thmgreenbox, name=Notation, numberwithin=section]{notation}
```

### Task 6: Test compilation
**Action**: Compile a single chapter to verify no errors
```bash
cd Notes/chapters
pdflatex ch02-type-theory-of-lean.tex
```

Check for:
- No LaTeX errors
- Colorful boxes appear correctly
- Text is readable
- Cross-references work

### Task 7: Compile full document
**Action**: Compile main document
```bash
cd Notes
pdflatex main.tex
bibtex main  # if using bibliography
pdflatex main.tex
pdflatex main.tex
```

### Task 8: Visual inspection
**Action**: Open `Notes/main.pdf` and verify:
- [ ] Theorems have blue rounded boxes
- [ ] Examples have red/salmon rounded boxes
- [ ] Remarks have black left-bar boxes
- [ ] Notation has green left-bar boxes
- [ ] All text is legible against backgrounds
- [ ] Box spacing looks good

### Task 9: Commit changes
**Action**: Git commit
```bash
git add Notes/preamble.sty
git commit -m "feat(latex): add Evan Chen style colorful theorem boxes

- Add mdframed, thmtools, tcolorbox packages
- Define 4 color styles: blue (theorem), red (example), green (notation), black (remark)
- Replace plain theorem environments with declaretheoremstyle
- Backup created at preamble.sty.backup-TIMESTAMP"
git push
```

---

## Rollback Plan

If something goes wrong:
```bash
cp Notes/preamble.sty.backup-TIMESTAMP Notes/preamble.sty
```

---

## Expected Changes Summary

**Before**: Plain black-and-white theorem environments  
**After**: 
- 🔵 Theorems/Lemmas/Propositions/Corollaries/Definitions → Blue rounded boxes
- 🔴 Examples/Exercises → Red/salmon rounded boxes  
- 🟢 Notation → Green left-bar boxes
- ⚫ Remarks → Black left-bar boxes

**Files modified**: 1 (`Notes/preamble.sty`)  
**Backup created**: 1 (`Notes/preamble.sty.backup-TIMESTAMP`)  
**New dependencies**: `mdframed`, `thmtools`, `tcolorbox`

---

## Notes

- The colorful style significantly improves readability and visual hierarchy
- Compatible with existing content (no changes needed to .tex chapter files)
- May need to adjust colors if printing in grayscale
- Box styles are customizable (can tweak colors, roundness, spacing)
