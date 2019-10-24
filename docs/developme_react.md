
### Setting up React App

1. `$ npm init react-app project-name` - creates a directory called project-name in the current working directory.
// Happy Hacking!

2. `$ cd project-name`

3. `$ npm start` - starts develeopment server and loads it up on google chrome

4. If using bootstrap, add `class="container"` on <body> on index.html.

# React

- All JS is in **/src/index.js**

- Import file App and use it for renedering inside root id.

- React component is a bit of html generated using JS

- `{}` = moustaches. They open up space to write JS within  HTML part of JSX. But can only write expressions(code that represents a value, so not a conditional but ternary operator OK because they equal a value). You can write all JS anywhere else in thes file

    eg. 10 < 20 ? "Duh" : "not maths";


- You can compartmentalise your code by using `import`. eg. create a js file for headers., copy over required code, change let App to let Header, add `export default Header`,in app.js add <Header />,   add `import Header from ./Header`. 


`./` = means something in the same directory


- Can't have two top-level components. Must use React fragments to encapsulate components.

eg. NO

```html
<Header />
<Content /> // wont work. need to wrap in div..

<div>
    <Header />
    <Content /> 
</div
```
YES

```html
or better yet use a <React.Fragment> like so

<>
    <Header />
    <Content /> 
<>
```

## Props

How to reuse components easily without manually changing them

```js
let Stuff = ({square}) => (

<>
    <Header>Rowl's App</Header>
    <Square colour="hotpink" /> // colour is a prop.
    <People />
    <Paragraph />
    <Clicked />   
</>
````

add arguments to your function in {}, give arguamnt value in the component.

One-way data flow


### EventS 

`on` key word indicates its an event listener

Click event:
```html
let Header = ({ children, subtitle} ) => (
  <>
    <h1 onClick={ () => console.log("hello") }>{ children }</h1>
    { subtitle ? <h2>{ subtitle }</h2> : null }
  </>
);
```

Move mouse event:
```html
let Header = ({ children, subtitle} ) => (
  <>
    <h1 onMouseMove={ () => console.log("hello") }>{ children }</h1>
    { subtitle ? <h2>{ subtitle }</h2> : null }
  </>
);
```

<input onChange={ () =>console.log}

Where we put event listerners:

Can't add EL to components in the App.js. has to be added to something that exist in the DOM (in the browser)

children. props. - is anythimng you put between the operning and closing tags of the component.


### STATE:

Using state with class components consists of three parts: • Setting up our initial state
• Displaying values based on this.state in our JSX
• Updating this.state when events are fired

Click event:
let counter = 0;

```js
class Header extends Component {

    constructor(props) //constructur to give initial value. Must also pass in extension values
    {
        super(props); // passes in the Components extenesion properties. Necessary to have for any inheritance required. which is all the time!

        this.state = {
            counter: 0; // this variable is the one we'll be keeping track off.
        };

        this.handleClick = this.handleClick.bind(this); // No need to understand, just do it    
    } 

    handleClick() {
        let current = this.state.counter;

        this.setState() {
            counter: current + 1, // cannot change state directly, need to do it through setState
            // be careful not to use the shorthand assignment operators like += and -=, as these will also update the value in the state.

        });
    }

    render() {
        let { children, subtitle ] = this.props;
        //Destructuring so we save properties to a variable;
        let { counter } = this.state;

        return (
            <>
                <h1 onClick={ this.handleClick }>{ children }</h1>
                { subtitle ? <h2>{ subtitle }</h2> : null }
                <p> { this.state.counter }</p>
            </>
        );
    }
}
````

When writing event listerners, you can shorthand props and save them to variables by destructuring them,

```js
next() {
        let { value } = this.state; // same as writing let current = this.state.value
        let { names } = this.props;
        this.setState ( 
            {value: (value + 1) % names.length}
        )    
    }
```

Lifting state = creating a parent component to store the states of children components. Taking the state of of it.

secret is - you pass down functions to the children components

### Routes:

a mapping between a URL and a piece of code to run.

make a route like this: <Route exact path='/' component={ Buttons } /> // in this case you need to write 'exact', because it is the root route.

exact means it is only what is contained in the quotes, but no exact means that it is any url starting that way.

Things not in a route will always show

to pass props to a component called by a route:

<Route path='/example' render{ () => <Figure props={ props } } />

use render{ () => <Component /> } to add props


### Matches:

<Route path='/articles/:id' render={ ({ match }) => (
  <Article article={ match.params.id } />
)}

matching allows us to match pages with urls that we don't have to explicitly declare

pass an object to render called match, and match.params.**example** gives us whatever is in the **example** wildcard defined in the path

this gets passed through as a prop to the component.

### Links

import Link from ReactRouter

//if you put a normal link, everything on the whole page reloads, which would wipe all state as the entire page is navigated away from to go to the link, even if it's an internal link.

use a link component: <Link to='/cats'>Cats!</Link> // or 'Router.Link' if you haven't imported it

<Route path="/squares/:colour" render={ ({ match }) => ( 
            <Squares colour={ match.params.colour } /> 
          )} />

The :id part of the URL is a parameter. can put anything there. 
the match.params.colour bit inserts whatever you but in the URL parameter into the child prop, in this case colour


404s:

import Switch from ReactRouter
import FourOhFour fom'./FourohFour';

wrap all components with Switch component:

const App = () => (
  <Router>
    <React.Fragment>
    <Header />
    <Switch>
      <Route path='/example' component={ Example } />
      <Route exact path='/' component={ Main } />
      <Route component={ FourOhFour } />
      // the last route with no path becomes the default if none of the others match
        <FourOhFour />
      </Switch>
    </React.Fragment>
  </Router>
)