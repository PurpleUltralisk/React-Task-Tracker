# Task Tracker App

Following Brad Traversy's [React Crash Course 2021](youtube.com/watch?v=w7ejDZ8SWv8).

## App Features

1. Passing state between components using react hooks
2. Use a mock JSON-Server as backend
3. Use react-router to mimic routes

## Getting Started with React

`$ npx create-react-app my-app`

## React Components

There are 2 ways we can write components:

1. Component as a Function

```javascript
export const Header = () => {
  return (
    <div>
      <h1>My Header</h1>
    </div>
  );
};
```

2. Component as a Class

```javascript
export default class Header extends React.Component {
  render() {
    return (
      <div>
        <h1>My Header</h1>
      </div>
    );
  }
}
```

We can then render this component or embed it into other components by

```javascript
<Header propName="My Title" />
```

## JSX

To write javascript in JSX, we can use `{}`.

## Passing Props

We pass in a prop to a component by doing

```javascript
<Header title="My Title" />
```

To use this prop the component will take in the prop as an argument

```javascript
export const Header = (props) => {
  return (
    <div>
      <h1>My Header</h1>
      <h2>{props.title}</h2>
    </div>
  );
};

// To set default prop
Header.defaultProp = {
  title: "Task Tracker",
};
```

## PropTypes

We can catch errors by using PropTypes or use Typescript

## useState

```javascript
import { useState } from "react";
const [tasks, setTasks] = useState();
```

`tasks` is what we want to call the state
`setTasks` is the function we will use to change the state
We set the default state inside the `useState()` brackets.

State is immutable.
So we cannot do something like `tasks.push()`.
Instead we have to use `setTasks()` to set the state.
Here we take advantage of the spread operator `setTasks([...tasks, {}])`

In this app we added a default tasks state at our App level.
Then we passed it down to our Task component:
`<Tasks tasks={tasks}/>`

## Passing state back up

**State get passed down, actions get passed up**
Redux and Context API can help achieve this.

We will use DeleteTask as an example.
We will first have a prop called onDelete.

At App.js level we render Tasks component.
We will also make a `deleteTask` function to get the id of the task we are trying to delete.
And we pass this function down in the form of a prop, so child components can send the id info back to App level.

```javascript
const deleteTask = (id) => {
  console.log("delete", id);
  setTasks(tasks.filter((task) => task.id !== id));
};

<Tasks tasks={tasks} onDelete={deleteTask} />;
```

The Tasks component will then take in this prop.
And then also pass this prop down to Task component.

```javascript
const Tasks = ({ tasks, onDelete }) => {
  return (
    <>
      {tasks.map((task) => (
        <Task key={task.id} task={task} onDelete={onDelete} />
      ))}
    </>
  );
};
```

Then Task component will also have access to this prop

```javascript
const Task = ({ task, onDelete }) => {
  return (
    <div className="task">
      <h3>
        {task.text}{" "}
        <FaTimes
          style={{ color: "red", cursor: "pointer" }}
          onClick={() => onDelete(task.id)}
        />
      </h3>
      <p>{task.day}</p>
    </div>
  );
};
```

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

## Build Project

`$ npm run build`
We can then deploy the `build` folder created by the command.
To test this:
`$ npm i -g serve`
`$ serve -s build -p 8000` Serves the `build` folder on port 8000.
