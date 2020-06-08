# react_node_heroku_deploy

## Deploying to Heroku
##### IMPORTANT: If your project is inside of an outer repo, you can't deploy it because you can't create a nested repo.  You'll need to move the project's folder outside of any existing repo before you can deploy.
You want to play Mastermind on your phone or have friends play it, right? Get it deployed! 
> It's recommended that you test the production app before deploying.  Again, do this by building the React app (`$ npm run build`) and browsing to `localhost:3001`.
With the MERN-stack app tested, we're **almost** ready to deploy to Heroku...
##### Add a `Procfile`
After the code has been uploaded using `git push heroku master`, Heroku checks to see if the project has a **Procfile** which specifies how to start up the application.
If no **Procfile** exists, Heroku will run the command assigned to the `start` script in **package.json**. Yes, we have a `start` script, but it's configured to start React's dev server instead of `node server.js`.
So yes, we need to create a **Procfile** (named exactly without a file extension):
- `$ touch Procfile`
Then, adding a single line inside **Procfile** takes care of informing Heroku how to boot our app:
```
web: node server.js
```
##### Update `package.json` to tell Heroku to Build the React App
The production-ready code that we tested out locally lives in the **build** folder. However, the **build** folder is git ignored and thus will not be pushed to Heroku.
The solution is to make Heroku run the build process immediately after it installs the node modules.
We do this by adding a `"heroku-postbuild": "npm run build"` entry inside of the `scripts` key in **package.json**:
```js
"scripts": {
  "start": "react-scripts start",
  "build": "react-scripts build",
  "test": "react-scripts test",
  "eject": "react-scripts eject",
  "heroku-postbuild": "npm run build"
},
```  
> Be sure to add a comma after the previous line.
 
Now Heroku will automatically run `npm run build` each time we deploy!
##### Create the App in your Heroku Account
Now let's use the Heroku CLI to create the project in your Heroku dashboard:
- `$ heroku create <optional_preferred_subdomain>`
The above command also creates a git remote named `heroku` that we push to in order to deploy.
Now you are set to deploy to Heroku:
1. Make a commit (if you haven't already): `$ git add -A && git commit -m "Deploy"`
2. Push to Heroku: `$ git push heroku master`
##### Set the Environment Variables on Heroku
The last step is to ensure that every KEY=VALUE pair in the `.env` file is set in the Heroku project.
No different than with the two previous projects deployed to Heroku. For each KEY=VALUE:
```
$ heroku config:set KEY=VALUE
```
##### Open the App
`$ heroku open` and now everyone can play the 1973 Game of the Year!
<img src="https://i.imgur.com/jyfJ4gy.png">
## Essential Questions
1. **What folder holds a React app's production-ready code?**
2. **Why does a "catch all" route need to be mounted in Express?** 
3. **True or False: API routes will need to be defined so that the React app can obtain data, create data in the database, etc.**
4. **True or False: The React app should use a "service" module to communicate with the backend's API routes via AJAX.**
