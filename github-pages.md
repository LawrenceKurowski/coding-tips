# Deploying your REACT app with Github Pages

## Basics (With `github.io` domain)
Follow [this](https://github.com/gitname/react-gh-pages?tab=readme-ov-file)

Github offers free domains that look like `username.github.io/reponame`.

Deploying in this case is like this:

1. Make a local directory where the project will live
   * this is where the site files will live.
   * this is **NOT** the repo corresponding to live deployment

You can push here to keep a up to date source of truth.

Whatever ChatGPT tells you, do NOT manually create `gh-pages` branch.

1. Make an empty Gtihub repo

    * for a free `github.io` domain, your github repo name MUST CONTAIN `github.io`. so for example `myrepo.github.io` is the repo name.
    * do not add readme or anything else.

1. Make new project with 
```bash
npx create-react-app my-app
```

1. `cd` to the `my-app`

1. do `npm install gh-pages --save-dev`

1. in `package.json` add this `"homepage": "https://gitname.github.io/git-repo-name"`
    * **NOTE** that for a standard, free page your repo name has to be 

1. in `package.json` -> `scripts` add this:
```bash
"predeploy": "npm run build",
"deploy": "gh-pages -d build",
```

1. link local dir with your empty repo
```bash
git init
git remote add origin https://github.com/{username}/{repo-name}.git
```

here you can add-commit-push to main if you'd like to keep copy.

* if this is github.io repo, dont forget to include this in repo-name above.

1. Build and test locally

Make a deploy-ready version
```bash
npm run build
```

deploy to local server with 
```bash
npm start
```
this will allow for live changes, so you can modify until production-ready.

1. push to prod:
```bash
`npm run deploy -- -m "added CNAME"`
```

This will
* push to the github new branch called `gh-pages`. This branch is created automatically
* push a publish-ready version

1. Configure github
In repo settings -> pages make sure it is set to serve from branch `gh-pages`

1. ongoing changes
re-build with `npm run build` and re-deploy with `npm run deploy`.


## Deploy to own domain
This one is funky

1. get the domain (e.g. squarespace)
1. in github settings -> pages -> custom domains input `www.yourdomain.com` so the www domain.
1. in domain DNS settings, input the following:

* CNAME record with host `www`, and target: `gitusername.github.io`
* 4xA records as follows:

```bash
@    8798    IN      A       198.49.23.144
@    8798    IN      A       198.185.159.144
@    8798    IN      A       198.185.159.145
@    8798    IN      A       198.49.23.145
```

1. add CNAME file
In your local dir add in `public` folder a file with filename `CNAME` (no extension) with just one line of content:
```bash
www.yourdomain.com
```

**NOTE** you should do this as opposed to manually creating a file in the repo at github.com. This is because as you push in the future using `npm run deploy`, CNAME will be eaten and site will return 404.

1. **important** Update homepage in `package.json` to your new domain in `https://` format


1. re-deploy and wait a few min

Should work.