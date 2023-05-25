
# README
## Purpose
This repo contains source code for the website https://informatica.nu/<br>
The site contains the programme for Computer Science students at Staniscollege Westplantsoen.
Teachers are being invited to look at https://informatica.nu/docenten/

## Edit
[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/scw-in/scw-in.github.io 
"Edit de content van deze site in Gitpod, je hebt dan een supersnelle preview van je wijzigingen zonder dat je iets hoeft te installeren")<br>

It is built on gohugo and the relearn theme.<br>
Content of the site can be found in /content

# How we created this site

## Create repo in github 
Create repo informatica.github.io in github and add any file (README.md is a good start)

Create replit.nix file
```
{ pkgs }: {
    deps = [
        pkgs.cowsay
        pkgs.hugo
    ];
}
```

Create .replit file
```
run = "hugo server"

[nix]
channel = "stable-22_11"
```

Create .gitpod.yml file
```
tasks:
  - before: brew install hugo
    command: hugo server
```

The command `hugo server` starts a webserver and continuously rebuilds the pages when one of the files is updated.

##  Import the repo in replit or gitpod
- `https://gitpod.nl/#https://github.com/SCW-IN/scw-in.github.io`
- `https://replit.nl/github/SCW-IN/scw-in.github.io`<br>
For replit, use the "blank repl"

## Create empty site with hugo
Install an empty hugo website with de shell command
```
hugo new site --force .
```

## Install relearn theme
Add relearn theme by 
1. adding files in /themes/hugo-theme-relearn
2. adding `theme = "hugo-theme-relearn"` to /config.toml

## Create first page on site
Create the first file /content/_index.md
```
First page, more content comes later
```

## Host the site
Deploy the de site on github

- Use github pages.<br>
See https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites
- Add a github action that runs hugo to update the site after each change. <br>
See https://gohugo.io/hosting-and-deployment/hosting-on-github/

## Edit the site
This repo works better in gitpod than in replit.

## Host the site on other domain
A bit of a hassle with github and the DNS records of your domain. This takes a day or so because the DNS changes need time to propagate through internet.<br>
See https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

## Documentation
- more info on using hugo in replit: <br>
https://docs.replit.com/tutorials/replit/build-host-company-blog-on-replit-with-hugo-nix
