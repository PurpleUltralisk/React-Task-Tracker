# Task Tracker App

Following Brad Traversy's [React Crash Course 2021](youtube.com/watch?v=w7ejDZ8SWv8).

## Notes

## Build Project

`$ npm run build`
We can then deploy the `build` folder created by the command.
To test this:
`$ npm i -g serve`
`$ serve -s build -p 8000` Serves the `build` folder on port 8000.

## Mock Backend

`$ npm i -g json-server`
Create a `db.json` file and "serve it" using `$ json-server --watch db.json`

Update `package.json` file `scripts` section with:

```javascript
"scripts":{
    "server": "json-server --watch db.json --port 5000"
}
```

Then we can call the server `$ npm run server`
