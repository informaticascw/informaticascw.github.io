Create repo informatica.github.io in github and add any file (README.md is a good start)
More info on naming the repo: https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites

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
Import the repo in replit

Install an empty hugo website with de shell command
'''
hugo new site --force .
'''

Import relearn theme by 
1.adding files in /themes/hugo-theme-relearn
2.adding 'theme = "hugo-theme-relearn"' to /config.toml

Create the first file /content/_index.html
'''
First page, more content comes later
'''

more info https://docs.replit.com/tutorials/replit/build-host-company-blog-on-replit-with-hugo-nix




Host de site on github
more info https://gohugo.io/hosting-and-deployment/hosting-on-github/
