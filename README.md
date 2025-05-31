# mystmd
Repository to start developing a book with MySTmd in a Codespace

## quickstart with this repo
1. Open this repositoy in Codespaces\
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/informaticascw/informaticascw.github.io?quickstart=1)
2. In the terminal, execute the command\
`bash start.sh`
3. Confirm popup to MyST-static files in browser

After editing files a reload of the webpages shows the result, `start.sh` automatically rebuilds html.

Output is shown in terminal. In case anything crashed, manually start `bash start.sh` again, old processed will be killed.

## how this repo was created
1. Create repository
2. Add devcontainer
3. Follow MyST Quickstart on https://mystmd.org/guide
4. Add deployment on github pages using terminal command `myst init --gh-pages` (first move book from subdir to root of repo)

Not done yet:
1. add LaTex for pdf (this can be done by adding a feature to the devcontainer)
2. add settings to make is easier for students (see examples in the github organisations StanislasSCW and Emmauscollege)

