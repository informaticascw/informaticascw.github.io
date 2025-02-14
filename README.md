
# README
## Purpose
This repo contains source code for the website https://stanislas.informatica.nu/<br>
The site contains some parts of the programme for Computer Science students at Staniscollege Westplantsoen.<br>
Teachers are being invited to look at https://stanisalas.informatica.nu/docenten/

## Edit
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/informaticascw/informaticascw.github.io?quickstart=1
"Edit de content van deze site in Codespaces, je hebt dan een supersnelle preview van je wijzigingen zonder dat je iets hoeft te installeren")<br>

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/scw-in/scw-in.github.io)

 [![Open in Codeanywhere](https://codeanywhere.com/img/open-in-codeanywhere-btn.svg)](https://app.codeanywhere.com/#https://github.com/scw-in/scw-in.github.io)


"Edit de content van deze site in Gitpod, je hebt dan een supersnelle preview van je wijzigingen zonder dat je iets hoeft te installeren")<br>

It is built on gohugo and the relearn theme.<br>
Content of the site can be found in /content

# How we created this site

## Create repo in github 
Create repo scw-in.github.io in github organisation scw-in and add any file (README.md is a good start)

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
run = "hugo server --buildDrafts --buildFuture --bind 0.0.0.0 --port 443 --disableLiveReload"

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
Editing this repo works better in gitpod than in replit.

Create the first file /content/_index.md
```
First page, more content comes later
```

## Host the site
Deploy the de site on github
- Add an action in github that runs hugo to update the site after each change. <br>
See https://gohugo.io/hosting-and-deployment/hosting-on-github/

## Host the site on other domain
A bit of a hassle with github and the DNS records of your domain. This may take multiple hours because the DNS changes need time to propagate through internet.<br>
See https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site

Don't forget:
1. add an A record (or cname record when you are using a subdomain) in the DNS of your domain.
2. add the domain to your repo (github -> repo -> settings -> pages)
3. add CNAME file in /content/static
4. add txt record in you DNS (github -> organisation -> settings ...) to verify your domain and thereby prevent other github organisations to use your domain

## Documentation
- more info on using hugo in replit: <br>
https://docs.replit.com/tutorials/replit/build-host-company-blog-on-replit-with-hugo-nix
