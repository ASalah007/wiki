# React 17: Getting Started

* in react we use jsk instead of html and then it is compiled using babel into js

* to render an Application you use `RenderDOM.render(<React Component>, document.getElementById('mountNode'))`
* a component in React is either a function or a class, for example:

```
function Button() {
  return <div> something</div>;
}
```
* you can use the component in jsx as `<Button />`
* the component must start with a capital letter or conflict with html/jsx elements might occur
* `useState(<value>)` defines a state and returns an array of two elements [<the elment itself>, <a setter function>]

* button jsx example:
```
function Button() {
  const [counter, setCounter] = useState(0);
  return <button onClick={handler}>{counter}</button>
}

function handler() {
  console.log(Math.random());
}
```

* if you want to render multible components you can ReactDOM.render([.., ..], ...) or `ReactDOM(<> .. .. .. </>, ...)`
* the empty tag is called React.Fragemen
* a component can use the its state elements and its parent's elements but not its children's or siblings'
* jsx style property: `style={ {color: Math.random()<0.8? 'red': 'green'} }`


## class components

```
class Comp extends React.Component {
  constructor (props) {
    super(props);
    this.state = {
      stateObject: 0,
      ...
    };
  }
  render(){
    return (
      <> ... </>
    );
  }
}
```

* for the cc to create state objects it must call the super(props) from the constructor and put its state objects 
  inside this.state 
  or 
  make a state class object by state ={};
  
  


* to reference an element inside a Componenet to use it elsewhere inside the same comp. you can use the ref object 
  first you create the ref element by `const ref = React.createRef()`
  then you attach it to the element you want to references insid the comp.
  `<h1 ref={this.ref}>...</h1>`

* or you can use states instead and the onChange={<function>};

