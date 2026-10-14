# Resume Tailoring Agent — Master Prompt (self-contained, OS-agnostic)

> Paste this whole file into any coding agent (OpenCode, Codex, Claude Code, Cursor, etc.) on
> **any OS (Windows / macOS / Linux)**. It is fully self-contained: it carries two complete,
> tested LaTeX templates **and** the person's full content of record, so it produces the same
> result even if the agent starts in an **empty folder** with no other files.
>
> If you are tailoring for a **different person**, replace §10 (Content of Record) and the
> `[Full Name]` placeholders. Everything else stays.

---

## 0. Scope & outcome

Given a **job description**, produce a tailored, ATS-friendly, **maximum 2-page** resume as
LaTeX, render it to PDF, verify it twice, and save it in a per-role folder. Never fabricate
facts. Never silently drop the person's real experience.

Two templates are provided (§6, §7). Both are **complete and compile as-is**.

---

## 1. Non-negotiable rules

1. **Never fabricate.** No invented metrics, employers, dates, titles, tools, or links. Use only
   §10 or what the user provides. If something is missing, **ask** or **omit**. Flag assumptions.
2. **2 pages maximum** (1 page only if the user asks). Never spill to a 3rd page.
3. **ATS first** — real selectable text, standard headings, no prose in tables, no text-in-images.
4. **Ask before assuming:** template choice, create-vs-modify, length, which
   projects/achievements to feature (§9).
5. **Reframe, don't erase.** When tailoring, reorder/rephrase; do not delete the person's roles
   unless asked. Every role they've held stays present.
6. **Render + verify twice** before claiming done (§8).
7. **Never change contact details** unless asked.
8. **Keep `\usepackage{etoolbox}`** in Template A — the footer uses `\patchcmd` and fails without it.
9. When asked to keep links "as icons", use FontAwesome icons as link text.
10. Commit / push only if the user asks.

---

## 2. Workflow (follow in order)

**Step 0 — Establish the working folder (OS-agnostic).**
- Work in the folder the user names. If none, create `<company> <role> resume/`:
  - macOS/Linux: `mkdir -p "<company> <role> resume"`
  - Windows PowerShell: `New-Item -ItemType Directory -Force "<company> <role> resume"`
- Assume **no other files exist**. All needed content is in §10. If resumes *do* exist nearby,
  cross-check facts against them, but §10 is the source of truth.

**Step 1 — Ask which template** (never assume): Template A or B (§6/§7). One-line each:
- **A** — RenderCV-style, two-column entries (`paracol`), one accent color, circled bullets. Compact/classic.
- **B** — Source Sans Pro, colored section headings, three-column education, highlighted metrics.

**Step 2 — Ask: create new, or modify an existing resume?** If modify, get the exact file path.

**Step 3 — Get the job description** (paste or link) and the **exact role title** for the PDF metadata,
plus anything not in §10 (new projects, links, metrics, awards).

**Step 4 — Ask the clarifying questions** (§9): length, projects/achievements
to feature, anything to omit.

**Step 5 — Tailor** (§4). Extract the JD's exact keywords; reorder; rewrite bullets outcome-first;
rebuild the Skills block to mirror the JD's categories.

**Step 6 — Write files** using §5 conventions; replace every `[Bracketed Placeholder]`.

**Step 7 — Compile to PDF** (§8.2).

**Step 8 — Verify twice** (§8.3). Fix and re-render until clean.

**Step 9 — Report:** what changed, what was reordered/reframed, assumptions flagged, page count,
remaining risks (e.g. location vs JD).

---

## 3. ATS rules

- Standard headings only: `Education`, `Experience`, `Projects`, `Skills`, `Achievements`,
  `Certifications`, `Positions of Responsibility`, `Languages`.
- Real text, never text-in-image; the PDF must be text-extractable.
- Keep the machine-readable preamble on (both templates already set `glyphtounicode` / `\pdfgentounicode=1`).
- One common font; escape special chars: `\%  \&  \#  \$  \_  \{  \}`.
- Dates: `Month YYYY – Month YYYY` (or `Present`), consistent format.
- Full, working hyperlinks. Spell out key acronyms once (e.g. "Retrieval-Augmented Generation (RAG)").
- Human, role-specific file name (§5). No emojis or decorative glyphs in body text.

---

## 4. Tailoring & framing rules

- **Mirror the JD's language** where truthful (e.g. "agentic workflows", "human-in-the-loop",
  "customer discovery", "deployments").
- **Outcome-first bullets:** *Action + what you built + metric + tools.* Put the number early.
  Example: "Grew X from 0 → 9,550 users (186%), 1,500+ paying, ₹3L+ revenue."
- **Answer the culture test.** If the JD values "high agency / ship fast / jump stacks", surface
  self-initiated projects and cross-stack work.
- **Order = relevance** (sections and bullets), while keeping dates accurate.
- **Skills block mirrors the JD categories**; list the JD's tools you genuinely have first.
- **No keyword-stuffing.** Every keyword sits inside a truthful claim.
- **No profile/objective section unless the user asks.**
- Trim filler so more real signal fits in 2 pages.

---

## 5. Output conventions

- **Folder:** `<company> <role> resume/` (e.g. `acme software engineer intern resume`).
- **Files:** `<first name> <company> <role> resume.tex` and the rendered `.pdf` of the same base name,
  side by side.
- **`pdftitle`:** `Jagadeesh Potupureddy's CV - <Role Title>`.
- **Footer (Template A):** `Jagadeesh Potupureddy - Page X of Y`.
- **Top-right note:** `Last updated in <Month Year>` (user's current month/year).
- **Keep** accent color `RGB(0, 79, 144)` unless asked to change it.
- Preserve the real header links (mailto, tel, LinkedIn, GitHub) exactly.
- Avoid filenames with `/ \ : * ? " < > |` (Windows-invalid). Spaces are fine.

---

## 6. Template A — RenderCV-style (complete, compiles as-is)

```latex
\documentclass[10pt, letterpaper]{article}

% =====================================================================
% TEMPLATE A - RenderCV-style two-column entries (paracol)
% Accent: primaryColor (deep blue). Bullets: small circles.
% Fill: replace every [Bracketed Placeholder]. Keep the preamble as-is.
% =====================================================================

% Packages:
\usepackage[
    ignoreheadfoot,
    top=2 cm,
    bottom=2 cm,
    left=2 cm,
    right=2 cm,
    footskip=1.0 cm,
]{geometry}
\usepackage{titlesec}
\usepackage{tabularx}
\usepackage{array}
\usepackage[dvipsnames]{xcolor}
\definecolor{primaryColor}{RGB}{0, 79, 144}
\usepackage{enumitem}
\usepackage{fontawesome5}
\usepackage{amsmath}
\usepackage[
    pdftitle={[Full Name]'s CV - [Role Title]},
    pdfauthor={[Full Name]},
    pdfcreator={LaTeX with RenderCV},
    colorlinks=true,
    urlcolor=primaryColor
]{hyperref}
\usepackage[pscoord]{eso-pic}
\usepackage{calc}
\usepackage{bookmark}
\usepackage{lastpage}
\usepackage{changepage}
\usepackage{paracol}
\usepackage{ifthen}
\usepackage{etoolbox} % required: \patchcmd is used for the footer
\usepackage{needspace}
\usepackage{iftex}

% Machine-readable / ATS-parsable output:
\ifPDFTeX
    \input{glyphtounicode}
    \pdfgentounicode=1
    \usepackage[utf8]{inputenc}
    \usepackage{lmodern}
\fi

% Settings:
\AtBeginEnvironment{adjustwidth}{\partopsep0pt}
\pagestyle{empty}
\setcounter{secnumdepth}{0}
\setlength{\parindent}{0pt}
\setlength{\topskip}{0pt}
\setlength{\columnsep}{0cm}
\sloppy
\hyphenpenalty=10000
\exhyphenpenalty=10000
\emergencystretch=3em
\makeatletter
\let\ps@customFooterStyle\ps@plain
\patchcmd{\ps@customFooterStyle}{\thepage}{
    \color{gray}\textit{\small [Full Name] - Page \thepage{} of \pageref*{LastPage}}
}{}{}
\makeatother
\pagestyle{customFooterStyle}

\titleformat{\section}{\needspace{4\baselineskip}\bfseries\large}{}{0pt}{}[\vspace{1pt}\titlerule]

\titlespacing{\section}{-1pt}{0.22 cm}{0.14 cm}

\renewcommand\labelitemi{$\circ$}
\newenvironment{highlights}{
    \begin{itemize}[
        topsep=0.10 cm,
        parsep=0.10 cm,
        partopsep=0pt,
        itemsep=0pt,
        leftmargin=0.4 cm + 10pt
    ]
}{
    \end{itemize}
}
\newenvironment{highlightsforbulletentries}{
    \begin{itemize}[
        topsep=0.10 cm,
        parsep=0.10 cm,
        partopsep=0pt,
        itemsep=0pt,
        leftmargin=10pt
    ]
}{
    \end{itemize}
}
\newenvironment{onecolentry}{
    \begin{adjustwidth}{0.2 cm + 0.00001 cm}{0.2 cm + 0.00001 cm}
}{
    \end{adjustwidth}
}
\newenvironment{twocolentry}[2][]{
    \onecolentry
    \def\secondColumn{#2}
    \setcolumnwidth{\fill, 5.0 cm}
    \begin{paracol}{2}
}{
    \switchcolumn \raggedleft \secondColumn
    \end{paracol}
    \endonecolentry
}
\newenvironment{header}{
    \setlength{\topsep}{0pt}\par\kern\topsep\centering\linespread{1.5}
}{
    \par\kern\topsep
}

\newcommand{\placelastupdatedtext}{%
  \AddToShipoutPictureFG*{%
    \put(
        \LenToUnit{\paperwidth-2 cm-0.2 cm+0.05cm},
        \LenToUnit{\paperheight-1.0 cm}
    ){\vtop{{\null}\makebox[0pt][c]{
        \small\color{gray}\textit{Last updated in [Month Year]}\hspace{\widthof{Last updated in [Month Year]}}
    }}}
  }%
}%

% Save and redefine \href so every link gets a small external-link icon.
\let\hrefWithoutArrow\href
\renewcommand{\href}[2]{\hrefWithoutArrow{#1}{\ifthenelse{\equal{#2}{}}{ }{#2 }\raisebox{.15ex}{\footnotesize \faExternalLink*}}}

\begin{document}
    \newcommand{\AND}{\unskip
        \cleaders\copy\ANDbox\hskip\wd\ANDbox
        \ignorespaces
    }
    \newsavebox\ANDbox
    \sbox\ANDbox{}

    \placelastupdatedtext
    \begin{header}
        \textbf{\fontsize{24 pt}{24 pt}\selectfont [Full Name]}

        \vspace{0.3 cm}

        \normalsize
        \mbox{{\color{black}\footnotesize\faMapMarker*}\hspace*{0.13cm}[City]}%
        \kern 0.25 cm%
        \AND%
        \kern 0.25 cm%
        \mbox{\hrefWithoutArrow{mailto:[email@example.com]}{\color{black}{\footnotesize\faEnvelope[regular]}\hspace*{0.13cm}[email@example.com]}}%
        \kern 0.25 cm%
        \AND%
        \kern 0.25 cm%
        \mbox{\hrefWithoutArrow{tel:[+91 0000000000]}{\color{black}{\footnotesize\faPhone*}\hspace*{0.13cm}[0000000000]}}%
        \kern 0.25 cm%
        \AND%
        \kern 0.25 cm%
        \mbox{\hrefWithoutArrow{[https://www.linkedin.com/in/handle/]}{\color{black}{\footnotesize\faLinkedinIn}\hspace*{0.13cm}[linkedin-handle]}}%
        \kern 0.25 cm%
        \AND%
        \kern 0.25 cm%
        \mbox{\hrefWithoutArrow{[https://github.com/handle]}{\color{black}{\footnotesize\faGithub}\hspace*{0.13cm}[github-handle]}}%
    \end{header}

    \vspace{0.3 cm - 0.3 cm}

    \section{Education}
    \begin{twocolentry}{
        \textit{[2023 -- 2027 (Expected)]}
    }
        \textbf{[Degree, Major]} \\
        \textit{[Institution, City]}
    \end{twocolentry}

    \vspace{0.10 cm}
    \begin{twocolentry}{
        \textit{[2021 -- 2023]}
    }
        \textbf{[Higher Secondary]} \\
        \textit{[School, City]}
    \end{twocolentry}

    \section{Experience}
    \begin{twocolentry}{
        \textit{[Location]} \\
        \textit{[Month Year -- Month Year]}
    }
        \textbf{[Job Title]} \\
        \textit{\href{https://example.com}{[Company]}}
    \end{twocolentry}
    \vspace{0.10 cm}
    \begin{onecolentry}
        \begin{highlights}
            \item [Achievement bullet: action + what you built + metric + tools.]
            \item [Achievement bullet with a hard number early.]
        \end{highlights}
    \end{onecolentry}

    \vspace{0.12 cm}
    \needspace{4\baselineskip}
    \begin{twocolentry}{
        \textit{[Location]} \\
        \textit{[Month Year -- Present]}
    }
        \textbf{[Job Title]} \\
        \textit{[Company]}
    \end{twocolentry}
    \vspace{0.10 cm}
    \begin{onecolentry}
        \begin{highlights}
            \item [Achievement bullet.]
        \end{highlights}
    \end{onecolentry}

    \section{Projects}
    \begin{twocolentry}{
        \textit{[Stack, Stack]}
    }
        \textbf{[Project Name]} \href{https://github.com/[handle]/[repo]}{\faGithub}
    \end{twocolentry}
    \vspace{0.10 cm}
    \begin{onecolentry}
        \begin{highlights}
            \item [What it does, who it is for, and the measurable outcome.]
        \end{highlights}
    \end{onecolentry}

    \section{Skills}
    \begin{onecolentry}
        \textbf{[Category]:} [skill, skill, skill] \\
        \textbf{[Category]:} [skill, skill, skill] \\
        \textbf{[Category]:} [skill, skill, skill]
    \end{onecolentry}

    \section{Achievements}
    \begin{onecolentry}
        \begin{highlights}
            \item [Achievement, with a number and a link if any.]
        \end{highlights}
    \end{onecolentry}

\end{document}
```

---

## 7. Template B — Source Sans Pro / colored headings (complete, compiles as-is)

```latex
\documentclass[10pt, letterpaper]{article}

% =====================================================================
% TEMPLATE B - Source Sans Pro, colored section headings, three-column
% education entries, metric highlighting. Fill [Bracketed Placeholders].
% Package fallbacks keep it compiling even without optional packages.
% =====================================================================

% Packages:
\usepackage[
    ignoreheadfoot,
    top=1.4 cm,
    bottom=1.4 cm,
    left=1.6 cm,
    right=1.6 cm,
    footskip=0.7 cm
]{geometry}
\usepackage{etoolbox}
\usepackage[explicit]{titlesec}
\usepackage{tabularx}
\usepackage{array}
\usepackage[dvipsnames]{xcolor}
\definecolor{primaryColor}{RGB}{0, 79, 144}
\usepackage{enumitem}
\usepackage{amsmath}
\usepackage[
    pdftitle={[Full Name]'s CV - [Role Title]},
    pdfauthor={[Full Name]},
    pdfcreator={LaTeX with RenderCV},
    colorlinks=true,
    urlcolor=primaryColor
]{hyperref}
\usepackage[pscoord]{eso-pic}
\usepackage{calc}
\usepackage{bookmark}
\usepackage{lastpage}
\usepackage{changepage}
\usepackage{paracol}
\usepackage{ifthen}
\usepackage{needspace}
\usepackage{iftex}
\usepackage{textcomp}

\ifPDFTeX
    \input{glyphtounicode}
    \pdfgentounicode=1
    \usepackage[T1]{fontenc}
    \usepackage[utf8]{inputenc}
    \IfFileExists{lmodern.sty}{\usepackage{lmodern}}{}
\fi

% Font: Source Sans Pro when available, otherwise a sans fallback.
\IfFileExists{sourcesanspro.sty}{
    \usepackage[default, type1]{sourcesanspro}
}{
    \usepackage{helvet}
    \renewcommand{\familydefault}{\sfdefault}
}

% Icons: FontAwesome 5 when available, otherwise silent fallbacks.
\IfFileExists{fontawesome5.sty}{
    \usepackage{fontawesome5}
    \newcommand{\iconLocation}{\faMapMarker*}
    \newcommand{\iconEmail}{\faEnvelope[regular]}
    \newcommand{\iconPhone}{\faPhone*}
    \newcommand{\iconLinkedIn}{\faLinkedinIn}
    \newcommand{\iconExternal}{\faExternalLink*}
}{
    \newcommand{\iconLocation}{}
    \newcommand{\iconEmail}{}
    \newcommand{\iconPhone}{}
    \newcommand{\iconLinkedIn}{}
    \newcommand{\iconExternal}{}
}

% Indian Rupee symbol with fallback.
\IfFileExists{tfrupee.sty}{
    \usepackage{tfrupee}
}{
    \providecommand{\rupee}{Rs.\,}
}

% Settings:
\AtBeginEnvironment{adjustwidth}{\partopsep0pt}
\pagestyle{empty}
\setcounter{secnumdepth}{0}
\setlength{\parindent}{0pt}
\setlength{\topskip}{0pt}
\setlength{\columnsep}{0.15cm}
\makeatletter
\let\ps@customFooterStyle\ps@plain
\patchcmd{\ps@customFooterStyle}{\thepage}{
    \color{gray}\textit{\small [Full Name] - Page \thepage{} of \pageref*{LastPage}}
}{}{}
\makeatother
\pagestyle{customFooterStyle}

\titleformat{\section}{
    \needspace{4\baselineskip}
    \large\color{primaryColor}
}{
}{
}{
    \textbf{#1}\hspace{0.15cm}\titlerule[0.8pt]\hspace{-0.1cm}
}[]

\titlespacing{\section}{
    -1pt
}{
    0.20 cm
}{
    0.12 cm
}

\newenvironment{highlights}{
    \begin{itemize}[
        topsep=0.05 cm,
        parsep=0.05 cm,
        partopsep=0pt,
        itemsep=0pt,
        leftmargin=0.4 cm + 10pt
    ]
}{
    \end{itemize}
}

\newenvironment{highlightsforbulletentries}{
    \begin{itemize}[
        topsep=0.05 cm,
        parsep=0.05 cm,
        partopsep=0pt,
        itemsep=0pt,
        leftmargin=10pt
    ]
}{
    \end{itemize}
}

\newenvironment{onecolentry}{
    \begin{adjustwidth}{0.2 cm + 0.00001 cm}{0.2 cm + 0.00001 cm}
}{
    \end{adjustwidth}
}

\newenvironment{twocolentry}[2][]{
    \onecolentry
    \def\secondColumn{#2}
    \setcolumnwidth{\fill, 4.5 cm}
    \begin{paracol}{2}
}{
    \switchcolumn \raggedleft \secondColumn
    \end{paracol}
    \endonecolentry
}

\newenvironment{threecolentry}[3][]{
    \onecolentry
    \def\thirdColumn{#3}
    \setcolumnwidth{1.5 cm, \fill, 4.5 cm}
    \begin{paracol}{3}
    {\raggedright #2} \switchcolumn
}{
    \switchcolumn \raggedleft \thirdColumn
    \end{paracol}
    \endonecolentry
}

\newenvironment{header}{
    \setlength{\topsep}{0pt}\par\kern\topsep\centering\color{primaryColor}\linespread{1.4}
}{
    \par\kern\topsep
}

\let\hrefWithoutArrow\href
\renewcommand{\href}[2]{\hrefWithoutArrow{#1}{\ifthenelse{\equal{#2}{}}{ }{#2 }\raisebox{.15ex}{\footnotesize \iconExternal}}}

\begin{document}
    \newcommand{\AND}{\unskip
        \cleaders\copy\ANDbox\hskip\wd\ANDbox
        \ignorespaces
    }
    \newsavebox\ANDbox
    \sbox\ANDbox{}

    \begin{header}
        \fontsize{26 pt}{26 pt}
        \textbf{[Full Name]}

        \vspace{0.25 cm}

        \normalsize
        [Degree, Major] ([Graduation Year]) \textbar{} [Target Role]

        \vspace{0.2 cm}

        \small
        \mbox{{\footnotesize\iconLocation}\hspace*{0.13cm}[City, State, Country]}%
        \kern 0.25 cm%
        \AND%
        \kern 0.25 cm%
        \mbox{\hrefWithoutArrow{mailto:[email@example.com]}{{\footnotesize\iconEmail}\hspace*{0.13cm}[email@example.com]}}%
        \kern 0.25 cm%
        \AND%
        \kern 0.25 cm%
        \mbox{\hrefWithoutArrow{tel:[+91-0000000000]}{{\footnotesize\iconPhone}\hspace*{0.13cm}[+91 0000000000]}}%
        \kern 0.25 cm%
        \AND%
        \kern 0.25 cm%
        \mbox{\hrefWithoutArrow{[https://linkedin.com/in/handle]}{{\footnotesize\iconLinkedIn}\hspace*{0.13cm}[linkedin-handle]}}%
    \end{header}

    \section{Professional Summary}
    \begin{onecolentry}
        [2-3 sentences: who you are, strongest role-relevant proof with one metric, and what you are
        seeking. Match the user's preference on first vs third person.]
    \end{onecolentry}

    \section{Education}
    \begin{threecolentry}{\textbf{[Degree Short]}}{
        [2023 -- 2027]
    }
        \textbf{[Institution]}, [City, Country]
        \begin{highlights}
            \item [Major] \textbar{} Current CGPA: \textbf{[9.0 / 10]}
            \item Relevant coursework: [Course, Course, Course]
        \end{highlights}
    \end{threecolentry}

    \section{Technical Skills}
    \begin{onecolentry}
        \textbf{Languages:} [Python, SQL, JavaScript, ...]
    \end{onecolentry}
    \vspace{0.12 cm}
    \begin{onecolentry}
        \textbf{Frameworks \& Libraries:} [Flask, React, ...]
    \end{onecolentry}
    \vspace{0.12 cm}
    \begin{onecolentry}
        \textbf{Databases \& Platforms:} [MongoDB, PostgreSQL, ...]
    \end{onecolentry}
    \vspace{0.12 cm}
    \begin{onecolentry}
        \textbf{Concepts:} [Web Development, System Architecture, ...]
    \end{onecolentry}
    \vspace{0.12 cm}
    \begin{onecolentry}
        \textbf{Tools:} [Git, Docker, Figma, ...]
    \end{onecolentry}

    \section{Technical Project}
    \begin{twocolentry}{
        [Academic Project]
    }
        \textbf{[Project Name]} -- [One-line description]
    \end{twocolentry}
    \begin{onecolentry}
        \textit{[Stack] \textbar{} [Stack] \textbar{} [Stack]}
    \end{onecolentry}
    \vspace{0.08 cm}
    \begin{onecolentry}
        \begin{highlights}
            \item [What problem it solves and for whom, with \textbf{bolded key terms} for ATS.]
            \item [A technical decision and why it mattered.]
            \item [Outcome or impact, with a number if possible.]
        \end{highlights}
    \end{onecolentry}

    \section{Experience}
    \begin{twocolentry}{
        [Location]

        [Month Year -- Present]
    }
        \textbf{[Company]}, [Title]
        \begin{highlights}
            \item [Scope + metric, e.g. served \textbf{4,000+ users} and generated \textbf{\rupee3,00,000+}.]
            \item [Ownership / leadership bullet.]
        \end{highlights}
    \end{twocolentry}

    \vspace{0.15 cm}

    \begin{twocolentry}{
        [Location]

        [Month Year -- Month Year]
    }
        \textbf{[Company]}, [Title]
        \begin{highlights}
            \item [Achievement bullet.]
        \end{highlights}
    \end{twocolentry}

    \section{Positions of Responsibility}
    \begin{onecolentry}
        \begin{highlights}
            \item \textbf{[Role, Org]} ([Year]): [What you led and the scale.]
        \end{highlights}
    \end{onecolentry}

    \section{Certifications}
    \begin{onecolentry}
        \begin{highlights}
            \item \textbf{[Issuer -- Certificate Name]}: [Detail / ID if any]
        \end{highlights}
    \end{onecolentry}

    \section{Achievements}
    \begin{onecolentry}
        \begin{highlights}
            \item [Award -- Competition, with a number or rank.]
        \end{highlights}
    \end{onecolentry}

    \section{Languages}
    \begin{onecolentry}
        [Language, Language, Language]
    \end{onecolentry}

\end{document}
```

---

## 8. Install, compile, verify (Windows / macOS / Linux)

### 8.1 Get a LaTeX engine (pick one)

**Tectonic (recommended — single binary, fetches packages on demand, best for agents):**
- macOS: `brew install tectonic`
- Windows: `winget install TectonicProject.Tectonic` — or `scoop install tectonic` / `choco install tectonic`
- Linux: `cargo install tectonic` — or your distro package / the GitHub release binary

**Full TeX distribution (also fine):**
- macOS: `brew install --cask mactex` (large)
- Windows: install **MiKTeX** (miktex.org) or **TeX Live**
- Linux: `sudo apt-get install texlive-full` (large) — or `texlive-latex-extra` + `texlive-fonts-extra`
  (the fonts-extra package provides `fontawesome5`; both templates need FontAwesome)

Confirm: `tectonic --version` **or** `pdflatex --version`.

> Note: Template A needs `fontawesome5`, `paracol`, `etoolbox`, `needspace`, `titlesec`, `eso-pic`,
> `lastpage`, `changepage`, `calc`, `bookmark`, `iftex`, `tabularx`. Tectonic fetches them automatically.

### 8.2 Compile (run in the resume folder; quote names with spaces)

```bash
# Preferred: Tectonic (any OS)
tectonic -X compile "jagadeesh acme software engineer resume.tex"

# Or latexmk (if a TeX distribution is installed)
latexmk -pdf -interaction=nonstopmode "jagadeesh acme software engineer resume.tex"

# Or pdflatex — RUN TWICE so \pageref*{LastPage} resolves
pdflatex -interaction=nonstopmode -halt-on-error "jagadeesh acme software engineer resume.tex"
pdflatex -interaction=nonstopmode -halt-on-error "jagadeesh acme software engineer resume.tex"
```
PowerShell: the same commands work; keep the double quotes. If `pdflatex` is missing and Tectonic
can't be installed, tell the user which engine to install — never hand back unrendered LaTeX.

### 8.3 Verify twice (both passes required)

**Pass 1 — machine checks (cross-platform, Python — recommended):**
```bash
pip install pypdf
python -c "from pypdf import PdfReader; r=PdfReader('jagadeesh acme software engineer resume.pdf'); print('PAGES:', len(r.pages)); [print('--- page', i+1, '---\n', (p.extract_text() or '')[:1500]) for i,p in enumerate(r.pages)]"
```
Alternative with Poppler (`pdfinfo` / `pdftotext` / `pdftoppm`):
- macOS: `brew install poppler` · Windows: `winget install oschwartz10612.Poppler` (or `choco install poppler`) · Linux: `sudo apt-get install poppler-utils`
```bash
pdfinfo "file.pdf"                     # expect Pages: 1 or 2, correct Title
pdftotext -layout "file.pdf" -          # ATS view: sections present, no mojibake
pdftoppm -png -r 110 "file.pdf" page    # -> page-1.png, page-2.png
```

**Pass 2 — human check:** open the rendered pages (or read `page-*.png`) and confirm:
- exactly 1–2 pages; no mid-entry page splits; nothing overflows the margins;
- header, icons and links render; dates consistent; footer correct.

### 8.4 Definition of done
- [ ] Compiles with **zero errors** (underfull-hbox warnings are fine).
- [ ] ≤ 2 pages.
- [ ] `pdftotext`/`pypdf` returns the full body text in a sensible order.
- [ ] PDF title = `Jagadeesh Potupureddy's CV - <Role>`.
- [ ] Every link is a real, working URL with the right text/icon.
- [ ] No fabricated facts; assumptions flagged to the user.
- [ ] `.tex` and `.pdf` live together in `<company> <role> resume/`.

---

## 9. Questions to ask the user (copy-paste)

> Before I build this, a few quick decisions:
> 1. **Template?** A (RenderCV/paracol — compact, classic) or B (Source Sans Pro, colored headings, 3-column education)?
> 2. **Create new, or modify an existing resume?** If modify, which file?
> 3. **Job description** — paste it (or the link) + the exact **role title**.
> 4. **Location** — confirm the current `City, State` to show in the header (never add "open to relocate" on the resume).
> 5. **Length** — 1 page or 2 pages?
> 6. **Which projects and achievements** should I feature, and anything to omit?
> 7. **Anything new** not in the content of record — new projects, links, metrics, awards, certificates?
> 8. **Source of truth** — use the content of record in §10, or will you paste fresh content?

Then: build → compile → verify twice → report changes and flagged assumptions.

---

## 10. Content of Record (self-contained — use as source of truth)

> Everything an agent needs. Never contradict these numbers; ask before changing any.

### Personal
- **Full name:** Jagadeesh Potupureddy
- **Location:** Visakhapatnam, India
- **Email:** jagadeeshpotupureddy@gmail.com
- **Phone:** +91 8688212827
- **LinkedIn:** https://www.linkedin.com/in/jagadeesh-potupureddy/
- **GitHub:** https://github.com/deadhearth01

### Education
- **B.Tech, Computer Science (Specialization in Cybersecurity)** — GITAM University, Visakhapatnam — **2023 – 2027 (Expected)**
- **12th Grade** — Narayana Junior College, Visakhapatnam — 2021 – 2023
- **10th Grade** — Ravindra Bharathi School, Visakhapatnam — Completed 2021

### Experience (newest first)

**1. Full Stack AI Engineering Intern — Evanrios Projects — Remote — June 2025 – January 2026**
- **LapromConnect** (lapromconnect.evanriosprojects.com): multilingual full-stack restaurant management system; React front end, Node.js/TypeScript back end; delivery, inventory, branch, stock and user management via RESTful APIs; English–Spanish i18n; comprehensive role-based access control.
- **Trigent AI dashboard** (app.trigentai.com): multi-agent system of three specialized AI agents (BI, AI, GX); autonomous business automation, market analytics, competitor analysis and growth prediction for enterprises; tool/API execution; human-in-the-loop oversight.
- **Glowbiz Displays** (glowbizdisplays.com): production platform for a Los Angeles digital-out-of-home ad network — advertiser campaign dashboard with artwork upload, human-in-the-loop ad review & approval workflow, QR-code generation, real-time scan/visit analytics.
- **Rioney Entertainment** (rioneyentertainment.in): production website for an entertainment enterprise client — separate admin, employee, client dashboards; integrated payment processing; secure credential sharing; project-management module.
- Testing: **Playwright** end-to-end for critical workflows (healthcare-grade reliability/security); documented code and API integrations.
- Worked via daily scrums, sprint planning, Git-based code reviews.

**2. Technical Lead — CHITTI — Visakhapatnam — September 2024 – Present**
- **CHITTI** (scorewithchitti.in): full-stack academic support platform; **9,550+ students**, **186% user growth**, **1,500+ paid subscribers** across 3 product iterations.
- Built an automated content pipeline for video editing and compression.
- Built an internal **SME (Subject Matter Expert) management dashboard** to onboard, coordinate and track contributors.
- **+25% engagement**; **₹3L+ revenue** from a premium subscription tier.

**3. Full Stack Developer — SUG Creative — Remote — September 2024 – Dec 2025**
- Full-stack multi-role management dashboard (sugcreative.com/login) for students, interns, clients and employees; per-role dashboards, task tracking, meeting scheduling.
- Centralized admin dashboard: payslips, certificates, administration of users/employees/mentors.
- Worked directly with clients across **10+ projects**, translating requirements into technical solutions; **100% satisfaction**.

**4. Web Designer and Developer — Young Compete — Remote — May 2024 – December 2024**
- Optimized site performance by **30%**; improved design; implemented full-stack features; **+20% engagement/retention**.
- Recognized **Top Performer of 2024**.

**5. Cybersecurity Intern — Intrainz — Remote — March 2024 – May 2024**
- Hands-on with Metasploit, Nmap, Linux and security frameworks.

### Projects
- **parda — Local PII Filter for AI Agents** — *Rust, Python, ONNX, ML* — https://github.com/deadhearth01/parda
  - Local, real-time privacy layer between users and AI agents (Claude Code, Codex, Anthropic/OpenAI SDKs, chat apps): names, contacts, Indian IDs (Aadhaar, PAN, GSTIN, UPI, IFSC) and secrets become format- and checksum-valid surrogates before leaving the machine, then are restored in answers and tool calls.
  - Three-tier detection: Aho-Corasick dictionary → checksum-validated rule packs → on-device GLiNER-PII ONNX NER (~9 ms p95). Fail-closed safety by default. Encrypted vault (XChaCha20-Poly1305, key in OS keychain). Streaming SSE rewriting restores values across split chunks.
  - Local proxy + clipboard hotkey; observability limited to kinds/counts/timings (never values); supply-chain CI (cargo-deny, e2e, coverage); Python fine-tuning/eval scripts.
- **Mitosis — Run Separate Copies of Mac Apps** — *Swift 6, SwiftUI, macOS* — https://github.com/deadhearth01/Mitosis
  - Native macOS 15+ app that runs separate copies of Mac apps side by side, each with its own login, data folder and Dock icon; APFS clone engine shares unchanged disk blocks (a copy costs a few MB).
  - Per-clone identity (own bundle ID/name); ad-hoc re-signing of only changed files; launch verification removes copies that fail to start; low-CPU background job rebuilds copies after the original updates without losing logins.
  - `mitosis` CLI (doctor/clone/list/stats/clean/refresh/delete); one-line installer with SHA-256 checksum + signature verification; automated release packaging.
- **Poshan (poshan-biomed)** — AI-powered child developmental & nutritional risk assessment app — https://github.com/deadhearth01/poshan-biomed *(optional feature)*
- **Decentralized Voting System** — blockchain e-voting, Solidity + biometrics — https://github.com/deadhearth01/decentralized-voting-system-R307S *(optional/older)*
- **AI Model Training Prototype** — LLM fine-tuning, PyTorch/FSDP, LoRA — https://github.com/deadhearth01/ai-model-prototype *(optional/older)*

### Skills (categories — reorder to mirror the JD)
- **Languages:** Python, TypeScript, JavaScript, Rust, Java, SQL, C
- **AI & ML:** PyTorch, TensorFlow, Hugging Face, ONNX Runtime, transformer/NER models, fine-tuning (LoRA), model evaluation, embeddings & vector search, RAG pipelines, prompt engineering, LLM integration
- **Agentic AI:** multi-agent orchestration, autonomous workflows, tool/function calling & API execution, persistent memory, human-in-the-loop safety, fallback protocols, observability, LangChain
- **Backend:** Node.js, Express.js, Python (Flask/Django), RESTful APIs, GraphQL, RBAC, event-driven services
- **Frontend:** React.js, Next.js, HTML5, CSS3, Tailwind CSS, Framer
- **Cloud & Infra:** AWS, Google Cloud, Docker, Kubernetes, CI/CD, Vercel, Firebase, GPU inference
- **Databases:** MongoDB, PostgreSQL, Supabase
- **Security & Privacy:** PII detection & redaction, on-device inference, encrypted storage (XChaCha20-Poly1305), RBAC, checksum validation
- **AI-Native Development:** Claude Code, Cursor, Codex, agentic coding
- **Testing & Tools:** Playwright, Git, GitHub, Postman, Figma, VS Code, Agile/Scrum
- **Robotics & Hardware (hobby):** Raspberry Pi 4, NVIDIA Jetson Nano, computer vision, voice-controlled physical AI, reverse engineering

> Only include lines that are true and relevant. If unsure, ask.

### Achievements
- **1st Runner-Up — Technovate** (India Student Conclave by Times of India), **₹40,000** prize — post: https://lnkd.in/p/dACwTd-S
- **2nd place — Bio Med Bharat**, **₹50,000** cash prize, for building an AI-powered child developmental & nutritional risk assessment app — post: https://lnkd.in/p/dA8nVGFw · certificate: https://creds.gitam.edu/c/28afb00f0dbd45a4b08b255631ef1d70 · repo: https://github.com/deadhearth01/poshan-biomed
- **2nd place — coding competition**, ₹5,000 prize, for building an AI mock test platform
- **Top Performer of 2024 — Young Compete**

### Certifications (include only if the role values them)
- Cybersecurity Essentials — Linux Foundation
- Introduction to Cybersecurity — Cisco
- ISC2 Systems Security Certified Practitioner (SSCP)

### Hobbies / interests (for narrative answers, or a one-line Skills entry)
- Hardware/robotics tinkering: Raspberry Pi 4 + NVIDIA Jetson Nano; voice-activated physical AI; object detection with a camera and pick/place with an arm, driven by plain-English commands.
- Reverse engineering and security research — finds vulnerabilities and writes exploits (own lab).
- Heavy, intentional daily use of AI coding agents to build and understand systems faster.

### Logistics
- Header location is always just the current **City, State** (e.g. `Visakhapatnam, Andhra Pradesh`). Never put "open to relocate" on the resume itself — handle relocation in the application form if asked.
