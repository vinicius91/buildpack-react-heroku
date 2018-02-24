Heroku Buildpack for create-react-app
=====================================

This is my customization from the original Heroku Buildpack from mars
For the original Repo:
[https://github.com/mars/create-react-app-buildpack]



Requires
--------

* [Heroku](https://www.heroku.com/home)
  * [command-line tools (CLI)](https://toolbelt.heroku.com)
  * [a free account](https://signup.heroku.com)
* [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [Node.js](https://nodejs.org)
* [create-react-app](https://github.com/facebookincubator/create-react-app)
  * `npm install -g create-react-app`

Quick Start
-----------


✏️ *Replace `$APP_NAME` with a name for your unique app.*

```bash
create-react-app $APP_NAME
cd $APP_NAME
git init
heroku create $APP_NAME --buildpack https://github.com/mars/create-react-app-buildpack.git
git add .
git commit -m "Start with create-react-app"
git push heroku master
heroku open
```


### Continue Development

Work with your app locally using `npm start`. See: [create-react-app docs](https://github.com/facebookincubator/create-react-app#getting-started)

Then, commit & deploy ♻️

### Push to Github

Eventually, to share, collaborate, or simply back-up your code, [create an empty repo at Github](https://github.com/new), and then follow the instructions shown on the repo to **push an existing repository from the command line**.

### Testing


[Heroku CI](https://devcenter.heroku.com/articles/heroku-ci) is supported with minimal configuration. The CI integration is compatible with npm & yarn (see [`bin/test`](bin/test)).

#### Minimal `app.json`

Heroku CI uses [`app.json`](https://devcenter.heroku.com/articles/app-json-schema) to provision test apps. To support Heroku CI, commit this minimal example `app.json`:

```json
{
  "buildpacks": [
    {
      "url": "https://github.com/vinicius91/buildpack-react-heroku"
    }
  ]
}
```

Customization
-------------


### Web server & Routing clean URLs

The web server may be [configured via the static buildpack](https://github.com/heroku/heroku-buildpack-static#configuration).

The default `static.json`, if it does not exist in the repo, is:

```json
{ "root": "build/" }
```

### Routing clean URLs

[React Router](https://github.com/ReactTraining/react-router) (not included) may easily use hash-based URLs like `https://example.com/index.html#/users/me/edit`. This is nice & easy when getting started with local development, but for a public app you probably want real URLs like `https://example.com/users/me/edit`.

Create a `static.json` file to configure the web server for clean [`browserHistory` with React Router v3](https://github.com/ReactTraining/react-router/blob/v3/docs/guides/Histories.md#browserhistory) & [`BrowserRouter` with v4](https://reacttraining.com/react-router/web/api/BrowserRouter):

```json
{
  "root": "build/",
  "routes": {
    "/**": "index.html"
  }
}
```
