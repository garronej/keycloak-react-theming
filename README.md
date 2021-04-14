<p align="center">
    <img src="https://user-images.githubusercontent.com/6702424/109354825-ab4b8e00-787e-11eb-8336-6009415ecaf6.png">  
</p>
<p align="center">
    <i>A template to assist you in creating and publishing TypeScript modules on NPM</i>
    <br>
    <br>
</p>

![image](https://user-images.githubusercontent.com/6702424/111089239-4012e480-852b-11eb-8351-df1610953d0c.png)

---

✅ NEW: The workflow is now fully portable.  
✅ NEW: Only one secret has to be defined: `NPM_TOKEN` (to enable publishing on your behalf on NPM).  
✅ NEW: `yarn` support  You are now free to use yarn instead of `npm` if you'd like to.  
✅ NEW: React ready ( `tsconfig.json` configured to transpile `.tsx` files).  

# Presentation

This template automates the boring and tedious tasks of:
- Filling up the ``package.json``
- Setting up Typescript.
- Writing a [README.md](https://github.com/garronej/ts_ci/blob/main/README.template.md) with decent presentation and instructions on how to install/import your module.
- Testing on multiple Node version running on Ubuntu and Windows before publishing.
- Maintaining a CHANGELOG.
- Publishing on NPM and creating corresponding GitHub releases.

Besides, good stuff that comes with using this template:
- The `dist/` directory is not tracked on the ``main`` branch.
- Shorter specific file import path.  
  ``import {...} from "my_module/theFile"`` instead of the usual
  ``import {...} from "my_module/dist/theFile"`` 
- CDN distribution for importing from an ``.html`` file with a ``<script>`` tag. (Optional, you can [disable](#disable-cdn-build) this feature for node projects)
- ESlint and Prettier are automatically run against files staged for commit. (Optional, you can [disable](#disable-linting-and-formatting) this feature)

If you want your module to support Deno as well checkout [denoify_ci](https://github.com/garronej/denoify_ci).
# Examples of project using this template

- [denoify](https://github.com/garronej/denoify)
- [keycloakify](https://github.com/garronej/keycloakify)
- [tss-react](https://github.com/garronej/tss-react)
- [EVT](https://github.com/garronej/evt) (uses [denoify_ci](https://github.com/garronej/denoify_ci) )

# Table of content

- [Presentation](#presentation)
- [Examples of project using this template](#examples-of-project-using-this-template)
- [Table of content](#table-of-content)
- [How to use](#how-to-use)
  - [Fork it ( click use the template )](#fork-it--click-use-the-template-)
  - [Enable automatic publishing](#enable-automatic-publishing)
- [Few things you need to be aware of before getting started](#few-things-you-need-to-be-aware-of-before-getting-started)
- [Customization:](#customization)
  - [Changing the directories structure](#changing-the-directories-structure)
  - [Swipe the image in the ``README.md``](#swipe-the-image-in-the-readmemd)
  - [Disable linting and formatting](#disable-linting-and-formatting)
    - [Disable Eslint and Prettier altogether](#disable-eslint-and-prettier-altogether)
    - [Disable only Prettier](#disable-only-prettier)
  - [Disable CDN build](#disable-cdn-build)
    - [Completely disable](#completely-disable)
    - [Only disable ES Module build ( ``dist/zz_esm/*`` )](#only-disable-es-module-build--distzz_esm-)
  - [Remove unwanted dev dependencies](#remove-unwanted-dev-dependencies)
  - [Customizing the Badges](#customizing-the-badges)
- [Accessing files outside the ``dist/`` directory](#accessing-files-outside-the-dist-directory)
- [The automatically updated ``CHANGELOG.md``](#the-automatically-updated-changelogmd)
- [Video demo](#video-demo)
- [Examples of auto-generated readme](#examples-of-auto-generated-readme)
- [Creating a documentation website for your project](#creating-a-documentation-website-for-your-project)
- [Creating a landing page for your project](#creating-a-landing-page-for-your-project)

# How to use

## Fork it ( click use the template )

- Click on ![image](https://user-images.githubusercontent.com/6702424/98155461-92395e80-1ed6-11eb-93b2-98c64453043f.png)
- The repo name you will choose will be used as a module name for NPM so:
  - Be sure it makes for a valid NPM module name.
  - Check if there is not already a NPM module named like that.
- The description you provide will be the one used on NPM and in ``package.json`` ( you can change it later )

Once you've done that a GitHub action workflow will set up the ``README.md`` and the ``package.json`` 
 for you, wait a couple of minutes for it to complete ( a bot will push ). You can follow the job advancement in the "Action" tab.

Each time you will push changes ``npm test`` will be run on remote docker containers against multiple node versions if everything passes you will get a green ``ci`` badges in your readme.

## Enable automatic publishing

Once you are ready to make your package available on NPM you 
will need to provide your NPM token so that the workflow can publish on your behalf:

Go to repository ``Settings`` tab, then ``Secrets`` you will need to add a new secret:
``NPM_TOKEN``, you NPM authorization token.

To trigger publishing edit the ``package.json`` ``version`` field ( ``0.0.0``-> ``0.0.1`` for example) then push changes... that's all !
The publishing will actually be performed only if ``npm test`` passes.  

# Few things you need to be aware of before getting started

- The files to include in the NPM bundle are cherry-picked using the ``package.json`` ``files`` field.  
  If you don't want to bother and includes everything just remove the ``files`` field from the ``package.json``.
- If you are going to programmatically load files outside of the ``dist/`` directory ( like the ``package.json`` or files inside ``res/`` ) be mindful that the paths might not be the one you expect. [Details](#accessing-files-outside-the-dist-directory). 
- The template does not support ``.npmignore`` ( it use the safer ``package.json`` ``files`` instead ).
- The template does not support ``.npmrc``.

# Customization: 

## Changing the directories structure

<details>
  <summary>Click to expand</summary>

You can freelly change how things are organized inside the `src/` directory but be mindfull:

- If you add a new directory in `src/`: Add it to `files` in `package.json` or it wont be included in you npm bundle.
- If you change the entry point of your module (default `src/index.ts`) update `include` in the `tsconfig.esm.json` as well as `main` and `type`
  in `package.json`.  
  
</details>

## Swipe the image in the ``README.md``

<details>
  <summary>Click to expand</summary>

A good way to host your repo image is to open an issue named ASSET in your project, close it, create a comment, drag and drop the picture you want to use and that's it. You have a link that you can replace in the ``README.md``.  
While you are at it submit this image as *social preview* in your repos github page's settings so that when you share on
Twitter or Reddit you don't get your GitHub profile picture to show up.

</details>

## Disable linting and formatting

### Disable Eslint and Prettier altogether

<details>
  <summary>Click to expand</summary>

Remove these ``package.json``'s ``scripts``:  

- ``_format``
- ``format``
- ``format:check``
- ``lint:check``
- ``lint``

Remove these ``package.j`on``'s ``devDependencies``:  
- ``prettier``
- ``eslint-config-prettier``  
- ``eslint``
- ``@typescript-eslint/parser``
- ``@typescript-eslint/eslint-plugin``
- ``husky``

Remove the  ``lint-staged`` and ``husky`` fields from the ``package.json``.  

Delete these files:  
- ``.prettierignore``
- ``.prettierrc.json``  
- ``.eslintignore``
- ``.eslintrc.js``

In ``.github/workflows/ci.yaml`` remove the ``test_lint`` job and the line ``needs: test_lint``.  

</details>

### Disable only Prettier

<details>
  <summary>Click to expand</summary>

[Prettier](https://prettier.io) is opinionated, it is OK to want to break free from it.

Remove these ``scripts`` from ``package.json``:  
- ``_format``
- ``format``
- ``format:check``

Remove these ``package.json``'s ``devDependencies``:  
- ``prettier``
- ``eslint-config-prettier``  

In the ``package.json``'s ``lint-staged`` field remove ``"*.{`s,json,md}": [ "prettier --write" ]``  

From ``.eslintrc.js``, remove the line: ``"prettier/@typescript-eslint",``.  

Delete these files:  
- ``.prettierignore``
- ``.prettierrc.json``  

In ``.github/workflows/ci.yaml`` remove the line ``npm run format:check`` from the ``test_lint`` job.  

</details>

## Disable CDN build  

### Completely disable  

<details>
  <summary>Click to expand</summary>

If your project does not target the browser or if you are not interested in offering CDN distribution:

- Remove all ``cdn:*`` npm scripts and ``npm run cdn`` from the `build` script ( in ``package.json`` ).
- Remove ``./tsconfig.esm.json``
- Remove ``simplifyify`` and ``terser`` from dev dependencies.

</details>

### Only disable ES Module build ( ``dist/zz_esm/*`` )  

<details>
  <summary>Click to expand</summary>

If ``npm run build`` fail because ``tsc -p tsconfig.esm.json`` gives errors you may want to remove the ESM
build but keep the ``bundle.js`` and ``bundle.min.js``. To do that:

In ``package.json`` replace theses ``scripts``:  

```json
{
  "cdn:bundle:.js": "simplifyify dist/index.js -s #{REPO_NAME}# -o dist/bundle.js --debug --bundle",
  "cdn:bundle:.min.js": "terser dist/bundle.js -cmo dist/bundle.min.js",
  "cdn:bundle": "npm run cdn:bundle:.js && npm run cdn:bundle:.min.js",
  "cdn:esm": "tsc -p tsconfig.esm.json",
  "cdn": "npm run cdn:bundle && npm run cdn:esm",
}
```

By theses ones:

```json
{
  "cdn:.js": "simplifyify dist/index.js -s #{REPO_NAME}# -o dist/bundle.js --debug --bundle",
  "cdn:.min.js": "terser dist/bundle.js -cmo dist/bundle.min.js",
  "cdn": "npm run cdn:.js && npm run cdn:.min.js",
}
```

Remove ``tsconfig.esm.json``. ( file at the root of the project )  

Edit the ``README.md`` to remove instructions about how to 
import as ES module.

</details>

## Remove unwanted dev dependencies

<details>
  <summary>Click to expand</summary>

Dev dependencies that are not required by the template ( you can safely remove them if you don't use them ):

- ``evt``
- ``@types/node``

Must keep:

- ``typescript``
- ``simplifyify`` ( for CDN build )
- ``terser`` ( for CDN build )

</details>

## Customizing the Badges

<details>
  <summary>Click to expand</summary>

You can use [shields.io](https://shields.io) to create badges on metrics you would like to showcase.

</details>

# Accessing files outside the ``dist/`` directory

<details>
  <summary>Click to expand</summary>

The drawback of having short import path is that the dir structure  
is not exactly the same in production ( in the npm bundle ) and in development.

The files and directories in ``dist/`` will be moved to the root of the project.  

As a result this won't work in production: 

``src/index.ts``
```typescript
import * as fs from "fs";
import * as path from "path";

const str = fs.readFileSync(
    path.join(__dirname,"..", "package.json")
).toString("utf8");
```

Because ``/dist/index.js`` will be moved to ``/index.js``

You'll have to do: 

``src/index.ts``
```typescript
import * as fs from "fs";
import * as path from "path";
import { getProjectRoot } from "./tools/getProjectRoot";

const str = fs.readFileSync(
    path.join(getProjectRoot(),"package.json")
).toString("utf8");
```

</details>

# The automatically updated ``CHANGELOG.md``

Starting from the second release, a ``CHANGELOG.md`` will be created at the root of the repo.

*Example:*  
![image](https://user-images.githubusercontent.com/6702424/82747884-c47a5800-9d9d-11ea-8f3b-22df03352e54.png)

The ``CHANGELOG.md`` is built from the commits messages since last release.

Are NOT included in the ``CHANGELOG.md``:
- The commit messages that includes the word "changelog" ( non-case sensitive ). 
- The commit messages that start with "Merge branch ".
- The commit messages that with "GitBook: "

*The GitHub release will point to a freezed version of the ``CHANGELOG.md``*:  
![image](https://user-images.githubusercontent.com/6702424/82748469-6439e500-9da2-11ea-8552-ea9b7322dfa7.png)

# Video demo

[![Watch the video](https://user-images.githubusercontent.com/6702424/82117367-c32ea700-976f-11ea-93f9-ec056aebc528.png)](https://youtu.be/Q5t-yP2PvPA)

# Examples of auto-generated readme

![npmjs com](https://user-images.githubusercontent.com/6702424/82402717-70017080-9a5d-11ea-8137-0bfa9a139655.jpg)

# Creating a documentation website for your project

I recommend [GitBook](https://www.gitbook.com), It enables you to write your documentation in markdown from their 
website and get the markdown files synchronized with your repo.
They will provide you with a nice website for which you can customize the domain name.  
All this is covered by their free tier.  

Example: 
- [repo](https://github.com/garronej/evt)
- [GitBook documentation website](https://docs.evt.land)

I advise you to have a special directory at the root of your project where the markdown documentation files
are stored. It is configured by placing a ``.gitbook.yaml`` file at the root of the repo containing, for example:
``root: ./docs/``  

Do not hesitate to request free access to premium features. Open source projects are eligible!  

PS: I am not affiliated with GitBook in any way.

# Creating a landing page for your project

Beside the documentation website, you might want to have a catchy landing page to share on social networks.  
You can use [GitHub pages](https://pages.github.com) to host it. 

If you like the landing page of EVT, [evt.land](http://evt.land), you can fork the [repo](https://github.com/garronej/evt.land) and adapt it for your module.  

To produce high quality GIF from screen recording that remain relatively small checkout the wonderful [Gifski](https://gif.ski) from [Sindre Sorhus](https://github.com/sindresorhus).

Once your page is ready you'll just have to go to settings and enable Pages yo put it online.

![image](https://user-images.githubusercontent.com/6702424/82155402-0aeb2680-9875-11ea-9159-f6167ee2928e.png)

And update your DNS: 

![image](https://user-images.githubusercontent.com/6702424/82155473-7e8d3380-9875-11ea-9bba-115cbb3ef162.png)

I personally use [Hurricane Electric](https://dns.he.net) free DNS servers because they support a lot of record types.
However, if your DNS provider does not support ``ALIAS``, you can use ``A`` records and manually enter the IP of GitHub servers.
I let you consult the [GitHub Pages Documentation](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain). 
