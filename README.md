# My resume

Software Engineer type resume Forked initially from *Sourabh Bajaj* at https://github.com/sb2nov/resume with modifications and more customization.

Feel free to use it for your own CV.

# Files

This resume template contains mainly the following list of files :

 1. **resume.tex**: Main document containing file;
 2. **Parts/Heading.tex**: Represents the heading section of the resume that contains personal information (Name, Role, Address, Email, Phone Numbers);
 3. **Parts/Sections/Employment.tex**: First section in the resume, describes the professional experience;
 4. **Parts/Sections/Education.tex**: Second section, describes the different educational institutions attended and the acquired degrees;
 5. **Parts/Sections/OtherExperience.tex**: Section containing non professional and outside school experience;
 6. **Parts/Sections/PrizesAndAwards.tex**: Here you put Prizes and Awards you won, including scholarships;
 7. **Parts/Sections/ProgrammingSkills.tex**: Listing group of skill sets;
 8. **Parts/Sections/Languages.tex**: Languages proficiency;  
 9. **Parts/Sections/Hobbies.tex**: Liked and practiced hobbies;
 10. **Parts/Sections/Links.tex**: Different links to website, blog, social media pages ...etc;
 11. **Commands.sty**: File that defines custom commands used withing the template;
 12. **Parameters.sty**: Used packages, fonts  

Additionally to these sections and parts, the author can add new section types.

# Compiling
This resume is written completely in Latex and must be compiled with **XeLatex** or **Lualatex**.

## Install Libraries
First install necessary libraries by installing tools such as [Miktex](https://miktex.org/download), [TexLive](https://tug.org/texlive/windows.html), or [ProTeXt](https://tug.org/protext/). These tools allow you to install a set of libraries related to latex and that are necessary to compile this code.

For MiKTeX for example, after installing it, open MikTeX console and click on check for updates on the Overview page. Then it will show you a message saying: "There are updates available! You can review the updates on the Updates page", then click on "Updates page".
Go then to Packages menu, click on the Update Db icon, filter by "Installed on", the select all non installed packages and lick on the "+" button to install them.

## Set receipes and tools
Set your latex receipes and tools, by editing your VSCode settings.json file and adding the following:

```yaml
"latex-workshop.latex.recipes": [
        {
            "name": "lualatex->biber->lualatex",
            "tools": [
                "lualatex"
            ]
        },
        {
            "name": "latexmk",
            "tools": [
                "latexmk"
            ]
        },
        {
            "name": "pdflatex -> bibtex -> pdflatex*2",
            "tools": [
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        }
    ],
    "latex-workshop.latex.tools": [
        {
            "name": "lualatex",
            "command": "lualatex",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "%DOC%"
            ]
        },
        {
            "name": "biber",
            "command": "biber",
            "args": [
                "%DOCFILE%"
            ]
        },
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
              "-synctex=1",
              "-interaction=nonstopmode",
              "-file-line-error",
              "-pdf",
              "-outdir=%OUTDIR%",
              "%DOC%"
            ],
            "env": {}
          },
          {
            "name": "pdflatex",
            "command": "pdflatex",
            "args": [
              "-synctex=1",
              "-interaction=nonstopmode",
              "-file-line-error",
              "%DOC%"
            ],
            "env": {}
          },
          {
            "name": "bibtex",
            "command": "bibtex",
            "args": [
              "%DOCFILE%"
            ],
            "env": {}
          }
    ],
    "latex-workshop.view.pdf.viewer": "tab",
```
# Preview 

<object data="https://github.com/AymenDaoudi/Resume/blob/master/resume.pdf" type="application/pdf" width="700px" height="700px">
    <embed src="https://github.com/AymenDaoudi/Resume/blob/master/resume.pdf">
        <p><a href="https://github.com/AymenDaoudi/Resume/blob/master/resume.pdf">Preview Resume</a>.</p>
    </embed>
</object>

# License

Format is MIT but all the data is owned by Aymen Daoudi.
