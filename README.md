
[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/scw-in/scw-in.github.io)<br>
Edit de content van deze site in Gitpod, je hebt dan een supersnelle preview.

This repo contains source code for the course Computer Engineering at Stanislascollege Westplantsoen, Delft, The Netherlands.

It is built on gohugo and the relearn theme.
Content of the site can be found in /content

The site is hosted at https://informatica.nu/
Teachers who want to re-use this site are being invited to look at https://informatica.nu/docenten/


# log of creating this site

## create repo in github
Create repo informatica.github.io in github and add any file (README.md is a good start)

Create replit.nix file
'''
{ pkgs }: {
    deps = [
        pkgs.cowsay
        pkgs.hugo
    ];
}
'''

Create .replit file
'''
run = "hugo server --buildDrafts --buildFuture --bind 0.0.0.0 --port 443 --baseURL https://informaticagithubio-vangeest.repl.co"

[nix]
channel = "stable-22_11"
'''

Create .gitpod.yml file
'''
tasks:
  - before: brew install hugo
    command: hugo server
'''

## Import the repo in replit or gitpod
For replit, use the "blank repl"

## create empty site with hugo
Install an empty hugo website with de shell command
'''
hugo new site --force .
'''

## install relearn theme
Import relearn theme by 
1.adding files in /themes/hugo-theme-relearn
2.adding 'theme = "hugo-theme-relearn"' to /config.toml

## create first page on site
Create the first file /content/_index.html
'''
First page, more content comes later
'''

## Host the site
Deploy the de site on github

- Use github pages. See https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites
- Add a github action that runs hugo to update the site after each change. See https://gohugo.io/hosting-and-deployment/hosting-on-github/

## Edit the site
This repo works better in gitpod than in replit.

## Documentation
- more info on using hugo in replit: https://docs.replit.com/tutorials/replit/build-host-company-blog-on-replit-with-hugo-nix