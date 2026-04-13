# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## Project Overview

This is a professional LaTeX resume for Aymen Daoudi, a Software Development Engineer based in Montreal, Quebec. The resume is structured as a modular LaTeX project with custom styling and commands.

## Repository Structure

```
Resume/
├── resume.tex              # Main document entry point
├── Parameters.sty          # Package imports and global configuration
├── Commands.sty            # Custom LaTeX commands for styling
├── resume.pdf              # Compiled output
├── Images/                 # Icons (HomeIcon.png, MessageIcon.png)
└── Parts/
    ├── Heading.tex         # Personal info header
    └── Sections/           # Individual resume sections
        ├── Employment.tex
        ├── Education.tex
        ├── Certifications.tex
        ├── Links.tex
        ├── PrizesAndAwards.tex
        ├── Languages.tex
        ├── Hobbies.tex
        ├── OtherExperience.tex      # Not currently included
        └── ProgrammingSkills.tex    # Not currently included
```

## Build Commands

Compile the resume using one of these methods:

```bash
# Preferred: LuaLaTeX (best font rendering)
lualatex resume.tex

# Alternative: XeLaTeX
xelatex resume.tex

# Alternative: pdfLaTeX (may have font limitations)
pdflatex resume.tex
```

For full compilation with bibliography support:
```bash
lualatex resume.tex && biber resume && lualatex resume.tex
```

## Key Architecture Decisions

### Modular Design
- **resume.tex**: Orchestrator that imports all sections via `\input{}`
- **Parameters.sty**: Centralizes all package imports and page geometry (1cm margins)
- **Commands.sty**: Defines all custom formatting commands
- **Parts/**: Content separated into individual section files for maintainability

### Document Configuration
- Document class: `article` with `letterpaper` size and `9pt` font
- Primary font: Roboto (light weight)
- Page geometry: 1cm margins on all sides
- Icon support: FontAwesome package

### Custom Commands Reference

| Command | Usage | Purpose |
|---------|-------|---------|
| `\Name{text}` | `\Name{John Doe}` | Large name display |
| `\RoleDescription{text}` | `\RoleDescription{Software Engineer}` | Job title styling |
| `\EmailAddresse{email}` | `\EmailAddresse{john@example.com}` | Email with icon |
| `\Addresse{address}` | `\Addresse{City, Country}` | Address with icon |
| `\PhoneNumbers{num}{}` | `\PhoneNumbers{555-1234}{}` | Phone with icon |
| `\WorkLocation{loc}` | `\WorkLocation{New York, NY}` | Location text |
| `\WorkPeriod{start}{end}` | `\WorkPeriod{Jan 2020}{\break Dec 2023}` | Date range |
| `\environment{tech}` | `\environment{Python, AWS, Docker}` | Tech stack box |
| `\resumeSubheading{title}{company}{location}{dates}` | See below | Job/education entry |
| `\resumeItem{label}{description}` | `\resumeItem{Led}{team of 5}` | Bullet point |
| `\resumeSubItem{prefix}{text}` | `\resumeSubItem{~~}{Detail}` | Sub-bullet |
| `\Certification{name}{issuer}{date}` | `\Certification{AWS}{Amazon}{2023}` | Cert format |
| `\LanguageSet{lang}{level}` | `\LanguageSet{French}{Native}` | Language entry |
| `\SkillSet{category}{skills}` | `\SkillSet{Backend}{Java, Python}` | Skill category |

### Common Patterns

**Adding a new job entry:**
```latex
\resumeSubheading
{Job Title,}{Company Name}{\WorkLocation{City, Country}}
{\WorkPeriod{Start Date}{\break End Date}}
  \resumeItemListStart
    \resumeItem{Achievement}{Description of what you accomplished}
    \begin{itemize}
      \resumeSubItem{~~}{Specific detail or metric}
      \resumeSubItem{~~}{Another specific detail}
    \end{itemize}
    \environment{Technologies: Tech1, Tech2, Tech3}
  \resumeItemListEnd
```

**Adding a new section:**
1. Create `Parts/Sections/NewSection.tex`
2. Add `\input{Parts/Sections/NewSection}` in `resume.tex`

## Conventions

- **Spacing**: Use negative `\vspace{}` values to tighten content (e.g., `\vspace{-10pt}`)
- **Indentation**: Custom `itemindent` values control bullet positioning
- **Sections**: All section titles are uppercase with horizontal rules
- **Hyperlinks**: Use `\href{url}{text}` for clickable links
- **Icons**: FontAwesome icons available via `\faIcon` commands
- **Page breaks**: Use `\pagebreak` when content needs to flow to next page

## Dependencies

- LaTeX distribution: MiKTeX, TexLive, or ProTeXt
- Required packages: roboto, fontawesome, tabularx, hyperref, geometry
- Recommended compiler: LuaLaTeX or XeLaTeX for best font rendering

## Files Currently Excluded

Two section files exist but are commented out in `resume.tex`:
- `OtherExperience.tex` - Additional work history
- `ProgrammingSkills.tex` - Technical skills breakdown

To enable: uncomment the corresponding `\input{}` lines in `resume.tex`.
