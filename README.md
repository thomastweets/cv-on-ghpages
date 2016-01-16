# CV on GitHub Pages that is compiled from LaTeX using TravisCI
With this repository you can show your CV using Git (obviously), LaTeX (beautiful type-setting, and a good portion of geekness), TravisCI (automatize all the things!), docker (keep build environments versionized), and GitHub pages (why host yourself?). In addition you can use a custom domain to host your CV (_e.g._ a subdomain).

## LaTeX template
Included is Alessandro Plasmati's [Classicthesis-Styled CV](http://www.latextemplates.com/template/classicthesis-styled-cv) template. You can exchange it for any LaTeX template you like that does not have dependencies that are not met by an updated [TeX Live](http://tug.org/texlive/) installation. Please see also the used [docker image](https://hub.docker.com/r/harshjv/texlive-2015/). However, the filename has to be "cv.tex".

## TravisCI
When you clone or fork this repository make sure that you enable it on [TravisCI](https://travis-ci.org).

### TravisCI API key
As Travis CI needs to be able to push to your GitHub repository (specifically the `gh-pages` branch) you need to authenticate it. As you do not want to store any passwords, ssh, or API keys in your repo or the TravisCI configuration the easiest way is to use the `travis` command line tool that is available as a gem to encrypt an Authentication Token for GitHub so that Travis CI can decrypt it when needed. First we need to install it:
```bash
# on OSX using the default Ruby installation
sudo gem install travis
```
Now we create a personal access token on GitHub to use with Travis CI. Follow [these instructions](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) to do so. I named mine `TravisCI cv-on-ghpages` and kept the standard scope settings. Copy the token when you created it as you will not be able to see it again after you close the page.
Encrypt the token with the `travis` command line tool:
```bash
# where 'your_token' is the token from the last step
travis encrypt GH_TOKEN=your_token
```
Copy the resulting key to line 18 of the `.travis.yml` file (replace `yoursecret` but keep the quotes):
```yml
env:
  global:
    - secure: "yoursecret"
```

## CNAME file (custom domain)
Change the `CNAME` file to your needs if you want to be able to redirect a custom domain name to your CV. Refer to [GitHub](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/) for help in setting up a corresponding DNS entry at your DNS provider.

## Finished
Now if you adapt the LaTeX template and push to your GitHub repository about 9 minutes later a beautiful PDF version of your CV will be visible at the domain _yourusername_.github.io/_yourrepositoryname_ or the custom domain name that you set. Congratulations and good luck with any job applications! :)

## License
The code is largely inspired by [travis-ci-latex-pdf](https://github.com/harshjv/travis-ci-latex-pdf) by [Harsh Vakharia](https://github.com/harshjv) (and the corresponding [blog post](http://harshjv.github.io/blog/document-building-versioning-with-tex-document-git-continuous-integration-dropbox/)).
This repository contains Alessandro Plasmati's [Classicthesis-Styled CV](http://www.latextemplates.com/template/classicthesis-styled-cv) template (License: [CC BY-NC-SA 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)).
