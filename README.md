# mystmd
Repository to start developing a book with MySTmd in a Codespace

## quickstart with this repo
1. Create Codespace from this repository
2. In terminal execute command `./start.sh`
4. Confirm popup to MyST-static files in browser

After editing files a reload of the webpages shows the result, `start.sh` automatically rebuilds html.

Output is shown in terminal. In case anything crashed, manually start `./start.sh` again, old processed will be killed.

## quickstart with this repo (old version)
1. Create Codespace from this repository
2. In terminal execute command `cd my-book`
3. In terminal execute command `myst start`
4. Confirm popup to show rendered book in browser with MyST-server
5. Edit files in /my-book to edit the book
6. Check output in preview of VSCode (many MyST features not supported)
7. Check output in browser with MyST-server
8. Double check output in browser with MyST-static by executing `myst build --html` and `npx -y http-server _build/html -c-1`
9. Push to github will deploy on github pages using `myst build --html`

## how this repo was created
1. Create repository
2. Add devcontainer
3. Follow MyST Quickstart on https://mystmd.org/guide
4. Add deployment on github pages using terminal command `myst init --gh-pages` (first move book from subdir to root of repo)

Not done yet:
1. add LaTex for pdf (this can be done by adding a feature to the devcontainer)
2. add settings to make is easier for students (see examples in the github organisations StanislasSCW and Emmauscollege)

