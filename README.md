# Task Tracker App

Following Brad Traversy's [React Crash Course 2021](youtube.com/watch?v=w7ejDZ8SWv8).

## Notes

## Build Project

`$ npm run build`
We can then deploy the `build` folder created by the command.
To test this:
`$ npm i -g serve`
`$ serve -s build -p 8000` Serves the `build` folder on port 8000.

## JSON-Server Backend

`$ npm i -g json-server`
Create a `db.json` file and "serve it" using `$ json-server --watch db.json`

Update `package.json` file `scripts` section with:

```javascript
"scripts":{
    "server": "json-server --watch db.json --port 5000"
}
```

Then we can call the server `$ npm run server`
See how we make GET, PUT, and DELETE requests.

## Routing

`$ npm i react-router-dom` to install router
To achieve routing, we need to use BrowserRouter and Route from this package.
Then we embed our components into a `<Router />` tag.

To disable the webpage from reload/refresh, replace `<a>` with `<Link />` tag.
