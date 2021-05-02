# Publish React App

Covers:

1. Netlify
2. Heroku

## Netlify

There are 2 ways we can deploy our application through Netlify.
One is to use the GUI, the other using `netlify-cli`.

### Setting up an account

1. Go to https://app.netlify.com/
2. Create an account, preferably using Github
3. Create a new team

### Option 1: GUI

1. Push the app to Github
2. on Netlify, select "New site from Git".
3. Under continuous deployment, select Github and authorities using 2FA if required
4. Select the repo to link with

### Option 2: Terminal

1. install `serve` and `netlify-cli` package

```sh
npm install -g serve netlify-cli
```

2. Build the react app

```sh
npm run build
```

```sh
serve -s build
```

3. Deploy to a temp Netlify server (publish directory: `./build`)

```sh
netlify deploy
```

4. Deploy to Netlify production (publish directory: `./build`)

```sh
netlify deploy --prod
```

Deploying an app that utilises react-router-dom: https://gist.github.com/sabrina-s/c0871264be2bb430d71a730d35015c56#deploying-with-react-router-dom

## Heroku

Signup a new account: https://signup.heroku.com/login

### Create a new application on Heroku website

On your [application dashboard](https://dashboard.heroku.com/apps), click the "New" button on top right corner and select "Create new app".

### Configure the buildpack for the application

Under the "Settings" -> "Buildpacks", add a buildpack for create-react-app with the following URL `https://github.com/mars/create-react-app-buildpack.git`.

What is a "buildpack"? Check the explanation [here](https://devcenter.heroku.com/articles/buildpacks)

### Configure the environment variables used by your application

If you build your React application using create-react-app, you can put some of the environment variables into .env file. During build and deployment, these environment variables would be filled into the HTML/JavaScript files that refers to those variables. You can read the [create-react-app documentation](https://create-react-app.dev/docs/adding-custom-environment-variables/) for more details.

However, some environment variables (e.g. the secret keys for calling those APIs) cannot be put into the .env files (because they are secret and should not be checked into code repository), you should declare those variables in Heroku.
On Heroku dashbaord, you can set this under "Settings" -> "Config Variables"
More documentation can be found [here](https://devcenter.heroku.com/articles/config-vars)

### Connect your Heroku app to the Github repository

- Click on Deploy tab → Deployment method → select GitHub
- Search for the repo of the application that you’re deploying → click Connect

![connect heroku app](_media/herokuConnectApp.png)

### Trigger a manual deploy

(Only for the first time deploying this app) click on “Deploy branch” at the end of the page
That's all! You can now visit the URL: https://randomly-generated-app-name.herokuapp.com/.
Subsequently, with every push to GitHub, your code is automatically deployed and accessible by anyone with internet access. Awesome!

### Resources

- For deploying `create-react-app` apps
  - https://blog.heroku.com/deploying-react-with-zero-configuration
  - [create-react-app-buildpack](https://github.com/mars/create-react-app-buildpack) (Browse the docs to understand what's going on and how you can add custom configuration)
- For deploying other node.js apps (e.g. server-side applications created with `express`)
  - https://devcenter.heroku.com/articles/getting-started-with-nodejs#introduction
  - https://devcenter.heroku.com/articles/deploying-nodejs
  - https://devcenter.heroku.com/articles/node-best-practices
