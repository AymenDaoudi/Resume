# Cover Letter Prompt

Reusable prompt for generating a cover letter from this resume and a job posting.
Paste the job description below the prompt, or point at it, and run.

---

## Prompt

You are writing a cover letter for Aymen Daoudi. Read the resume first, at the repo
root one level up from this folder (`../Parts/Heading.tex`, `../Parts/Sections/*.tex`),
and use it as the only source of facts about him. A job description follows this
prompt. Everything you produce belongs in this `CoverLetters/` folder.

### Hard rules

- **Invent nothing.** Every factual claim about experience, employers, technologies,
  timelines, titles, education or results must be traceable to a line in the resume.
  If the posting asks for something not on the resume, leave it out. Do not fill gaps
  with plausible-sounding detail, and do not fabricate anecdotes or specific incidents.
- **Do not exaggerate.** Keep the resume's own wording strength. "Helped build" does not
  become "built". "Contributed to" does not become "led". Round years down, not up.
- **It must read as written by a person**, not generated. Plain, direct sentences.
  No breathless enthusiasm, no thought-leader aphorisms, no corporate filler.
- **Keep it short.** Roughly 350–420 words, four body paragraphs plus a closing. It
  has to fit one page with clear white space left at the bottom. If the text runs to
  the footer, it is too long, and the fix is cutting words rather than shrinking type.
- **The resume carries the detail.** The letter's job is to say what he did and why
  this role fits, not to restate the resume in prose.

### Structure

**Paragraph 1 — the application and why it interests him.**
State plainly which role he is applying for and where. Then say why it is interesting
to him, tying something real about the company or the product to something real about
his own work or motivation. Genuine interest, not flattery of the company.

**Paragraph 2 — current role at Numa. Keep it brief.**
Take the emphasis from what the posting actually asks for. Numa offers several
different angles and only one should lead:
- **AI postings** — AI running in production rather than in demos (models in the live
  call flow, latency, failure handling, keeping the agent within safe boundaries),
  plus AI tooling in his own development work (Cursor, Claude Code).
- **Backend or platform postings** — the Python work (Django, FastAPI, Flask) over
  Postgres, the integration layer, and production ownership: watching live traffic,
  tracing failures back through the stack, fixing them at the source.
- **Integration or operations postings** — the dealer management system work, led on
  Reynolds & Reynolds, and the loop from a production failure back into the integration.
Whatever leads, give the others a clause at most. Do not default to the AI angle
because it is the most interesting; default to the one the posting is hiring for.
Close the paragraph by connecting the emphasis directly to what the posting asks for.

**Paragraph 3 — earlier experience, at altitude. Keep this the shortest body paragraph.**
Say what he *did*, not what he did it *with*. No deep detail, no project-by-project
tour. Cover:
- the **verticals** he has worked in (facilities maintenance, EV charging, maritime
  compliance, financial policy and insurance, pharma, research);
- the **nature of the work**, in plain terms: designing distributed backend systems,
  keeping them maintainable as they grow, improving how teams ship.
Then the MSc from UQAM and the SAC'19 publication.

**Do not list technologies in this paragraph.** No stack enumerations, no runs of
language, database or framework names. The resume already carries all of that, and
repeating it swells the paragraph without adding anything a reader will use. Naming a
single technology is fine where it is load-bearing for the point being made, but a
roll-call is not.

**Paragraph 4 — why this team and this company, and willingness to contribute.**
Return to the specific team and what makes it appealing. State concretely what he is
ready to contribute: ownership of features end to end, reviewable design documents,
code review, helping teammates onboard. Mention that he is based in Montréal and has
worked remotely with US teams since 2022 where remote work is relevant.

**Closing — formal and respectful.**
Thank the reader for their time and consideration, offer to discuss further, and sign
off with a formal valediction ("Respectfully," or "Sincerely,") above his name.

### Header

Open the letter with his contact block and the date, then a formal salutation
addressed to the company's hiring team:

```
Aymen Daoudi
Montréal, Québec
iaymendaoudi@gmail.com | +1 438 927 9580
linkedin.com/in/aymendaoudi

<date>

Dear <Company> Hiring Team,
```

### Language to avoid

These read as machine-written or as filler. Do not use them:

- "I am thrilled / excited / passionate about…"
- "aligns with your mission", "resonates with me", "I was drawn to…"
- "leverage", "spearheaded", "delve", "robust", "cutting-edge", "seamless",
  "dynamic environment", "proven track record", "wealth of experience"
- "I believe I would be a great fit"
- Strings of three parallel items used for rhythm rather than meaning
- Heavy em-dash use; prefer commas, colons and full stops
- Quotable one-line aphorisms; make at most one point of view per letter, and only
  one that his actual work supports

### Output

Name every file `CoverLetter_<Company>_<Role>`, with the company and role in
PascalCase and no spaces, e.g. `CoverLetter_Point_SeniorSoftwareEngineer`. Use that
same base name for the `.md`, the `.tex` and the `.pdf` so an application's three
artefacts sort together. Write the finished letter to the `.md`, then typeset it as a
PDF. Flag any requirement in the posting that the resume does not support, so it can
be decided separately whether to address the gap.

Keep the `.md` and the `.tex` in sync. Edits made while tightening tend to land in the
`.tex` only, which silently leaves the `.md` holding an older draft.

### PDF

Copy `CoverLetter_Point_SeniorSoftwareEngineer.tex` to the new base name and swap the
body text, escaping LaTeX specials as you go (`&` → `\&`, `#` → `\#`, `%` → `\%`). It reuses the
resume's `Parameters.sty` and `Commands.sty` so the two documents look like a matched
set. Four overrides in that file are load-bearing and must survive any edit:

- **Paths to the repo root.** The style files and `Images/` live one level up, so the
  preamble sets `\input@path` to `{../}` before `\usepackage{Parameters}` and
  `\graphicspath{{../}}` after it. The order matters: `graphicx` is loaded by
  `Parameters.sty`, so `\graphicspath` cannot come first. Without these the build
  fails on a missing style file or drops the header icons.
- **Justified body text.** `Parameters.sty` issues a global `\raggedright` for the
  resume layout. The letter is justified, so that is undone after `\begin{document}`
  with `\rightskip=0pt`, `\leftskip=0pt` and `\parfillskip=0pt plus 1fil`, and
  `microtype` is loaded to keep inter-word spacing even. `\parindent` stays at `0pt`
  for block paragraphs.
- **Roboto document-wide.** `\roboto` is a declaration, not a wrapper.
  `Commands.sty` issues it inside every macro, which is the only reason the resume
  renders in Roboto; the document default is still the Latin Modern serif. The letter
  needs a bare `\roboto` after `\begin{document}`, or the prose silently comes out
  serif and stops matching the resume.
- **Letter geometry.** 10pt with 2.6cm margins, not the resume's 9pt and 1cm. A 1cm
  margin gives a ~19.6cm measure that is punishing for running prose; the resume only
  gets away with it by confining everything to `0.82\textwidth` parboxes.

Build with (MacTeX is installed but is not on the shell PATH by default):

```bash
export PATH="/Library/TeX/texbin:$PATH"
cd CoverLetters
lualatex -jobname=CoverLetter_<Company>_<Role> CoverLetter_<Company>_<Role>.tex
```

Before delivering, grep the log for `Overfull` and `Underfull`, confirm the output is
one page, and look at the rendered page to check it does not run to the footer.
