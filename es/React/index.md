# React (Basado en el curso de FreeCodeCamp)
React usa una extensión de sintaxis de JavaScript llamada **JSX** que te permite escribir HTML directamente dentro de JavaScript. Esto tiene muchos beneficios.  
Te permite utilizar el poder programático completo de JavaScript dentro de HTML, y ayuda a mantener tu código legible.  

```const JSX = <h1>Hello JSX!</h1>;```

---

Dentro del JSX solo se puede devolver un elemento, de forma que el siguiente código daría error:
```javascript
const JSX = <h1>Hello JSX!</h1> <p>Some info</p>;
```

Para su correcto uso se debe envolver en un elemento padre:
```javascript
const JSX = <div><h1>Hello JSX!</h1> <p>Some info</p></div>;
```

Para colocar compentarios de hacer con la expresión {/* */}:
```javascript
const JSX = (
  <div>
    {/* No deben ser modificados */}
    <h1>This is a block of JSX</h1>
  </div>
);
```

---

**ReactDOM** ofrece un método simple para renderizar elementos React al DOM que se ve así: ```ReactDOM.render(componentToRender, targetNode)```:
* El primer argumento es el elemento o componente React que deseas renderizar
* El segundo argumento es el nodo DOM al que se quiere renderizar el componente.

---

Una diferencia clave en JSX es que ya no puedes usar la palabra class para definir clases HTML. Esto es debido a que class es una palabra reservada en JavaScript. En su lugar, JSX utiliza **className**.

De hecho, la convención de nomenclatura para todos los atributos HTML y referencias a eventos en JSX se convierte a **camelCase**. Por ejemplo:
* Un evento de clic en JSX es **onClick**, en lugar de onclick.
* onchange se convierte en **onChange**.
Si bien se trata de una diferencia sutil, es importante tenerlo en cuenta.

---

React requiere que tu nombre de función comience con una letra mayúscula. Esto diferencia los componentes React de las etiquetas HTML normales. Por ejemplo, ```<div />``` representa una etiqueta HTML, pero ```<Welcome />``` representa un componente y requiere que Welcome sea una función de React.
```javascript
const MyComponent = function() {
  let string = "Hola"
  return (
    <div>{string}</div>
  )
}
```

--- 

## Crear un componente
Los componentes son las piezas fundamentales de React. Un componente es una parte de la interfaz de usuario (UI) que se puede reutilizar. Los componentes se pueden pensar como cajas de herramientas independientes que contienen código que puede usar en su aplicación.
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div>
        <h1>My First React Component!</h1>
      </div>
    );
  }
};

ReactDOM.render(<MyComponent />, document.getElementById('challenge-node'))
```

--- 
## Información de padre a hijo

Para pasar información de un componente padre a un componente hijo se usan las **props**, 
```javascript
const CurrentDate = (props) => {
  return (
    <div>
      <p>The current date is: {props.date}</p>
    </div>
  );
};
```

---
 Si queremos asignarle unos valores por defecto, en caso de que no se le pase nada, se hace con **defaultProps**:
 ```javascript
 const CurrentDate = (props) => {
  return (
    <div>
      <p>The current date is: {props.date}</p>
    </div>
  );
};
CurrentDate.defaultProps = { date: 'Unknown' };
```

En la mayoría de circunstancias deberíamos ver:
```javascript
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}
//Propieades por defecto
Items.defaultProps = { quantity: 0 }

class ShoppingCart extends React.Component {
  constructor(props) { super(props); }
  //Asignación de propiedades
  render() { return <Items quantity={10}/> }
};
```

## Propiedades obligatorias
Para obligar a que se pasen unas propiedades se usa **propTypes**:
```javascript
const Items = (props) => {
  return <h1>Current Quantity of Items in Cart: {props.quantity}</h1>
}
//Propieades por defecto
Items.defaultProps = { quantity: 0 }
//Propiedades obligatorias
Items.propTypes = { quantity: PropTypes.number.isRequired }
```
---

En caso de ser una clase que no sea con flecha, se hace de la siguiente forma:
```javascript
class App extends React.Component {
  constructor(props) {super(props);}
  render() {
    return (<div><Welcome name={"Nano"}/></div>);
  }
};

class Welcome extends React.Component {
  constructor(props) {super(props);}
  render() {
    return (<p>Hello, <strong>{this.props.name}</strong>!</p>);
  }
};
```
---

## Estados (Basico)
(Es una forma de tener datos dentro de una clase/componente)
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: 'freeCodeCamp' }
  }
  render() {
    let name = this.state.name;
    return ( <div><h1>{name}</h1></div> );
  }
};
```

Para cambiar un valor de un estado se usa **this.setState()**:
<!-- tabs:start -->

<!-- tab:Ejemplo 1 -->
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: 'Initial State' };
    this.handleClick = this.handleClick.bind(this);
  }
  handleClick() {
    this.setState({ name: 'React Rocks!' });
  }
  render() {
    return (
      <div>
        <button onClick={this.handleClick}>Click Me</button>
        <h1>{this.state.name}</h1>
      </div>
    );
  }
};
```

<!-- tab:Ejemplo 2 -->

```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { visibility: false };
    this.toggleVisibility = this.toogleVisibility.bind(this)
  }

  toogleVisibility(){
    this.setState(state => ({visibility: !state.visibility}));
  }

  render() {
    if (this.state.visibility) {
      return (
        <div>
          <button onClick={this.toggleVisibility}>Click Me</button>
          <h1>Now you see me!</h1>
        </div>
      );
    } else return (<button onClick={this.toggleVisibility}>Click Me</button>);
  }
}
```

<!-- tab:Ejemplo 3 -->
```javascript
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
    
    this.increment = this.increment.bind(this)
    this.decrement = this.decrement.bind(this)
    this.reset = this.reset.bind(this)
  }

  increment(){ this.setState(state => ({count: ++state.count})); }
  decrement(){ this.setState(state => ({count: --state.count})); }
  reset(){ this.setState({count: 0})}

  render() {
    return (
      <div>
        <button className='inc' onClick={this.increment}>Increment!</button>
        <button className='dec' onClick={this.decrement}>Decrement!</button>
        <button className='reset' onClick={this.reset}>Reset</button>
        <h1>Current Count: {this.state.count}</h1>
      </div>
    );
  }
};
```

<!-- tabs:end -->

---

## Interactuar con inputs
```javascript
class ControlledInput extends React.Component {
  constructor(props) {
    super(props);
    this.state = { input: '' };
    this.change = this.change.bind(this)
  }
  change(v){
    this.setState({input:v.target.value})
  }
  render() {
    return (
      <div>
        <input onChange={this.change} value={this.state.input}/>
        <h4>Controlled Input:</h4>
        <p>{this.state.input}</p>
      </div>
    );
  }
};
```

---

Al igual que en Angular tenemos los distintos ciclos de vida de un componente, en React existen funciones con el mismo propósito:
* **componentWillMount()** se llama antes de que se monte el componente.
* **componentDidMount()** se llama después de que se monte el componente.
* **componentWillReceiveProps()** se llama cuando el componente recibe un nuevo conjunto de props.
* **shouldComponentUpdate(nextProps, nextState)** se llama antes de que se actualice el componente.
* **componentWillUpdate()** se llama antes de que se actualice el componente.
* **componentDidUpdate()** se llama después de que se actualice el componente.
* **componentWillUnmount()** se llama después de que se desmonte el componente.
* **componentDidCatch()** se llama cuando un error ocurre en cualquier componente secundario anidado en el árbol.
  

## (ngIf) Ocultar un componente
```javascript
class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    this.state = { display: true }
    this.toggleDisplay = this.toggleDisplay.bind(this);
  }
  toggleDisplay() { this.setState(state => ({ display: !state.display })); }
  render() {
    return (
       <div>
         <button onClick={this.toggleDisplay}>Toggle Display</button>
         {this.state.display && <h1>Displayed!</h1>}
       </div>
    );
  }
};
```

---
# Ejercicios
## Ejercicio X
Chequear la edad y colocar un único boón que vaya cambiadno en función de la edad insertada.  

(Enunciado real)
El editor de código tiene tres constantes definidas dentro del método render() del componente CheckUserAge. Estas se llaman buttonOne, buttonTwo y buttonThree. A cada una de estas se le asigna una expresión JSX simple que representa un elemento de botón. Primero, inicializa el estado de CheckUserAge con input y userAge ambos configurados a valores de una cadena vacía.
Una vez que el componente está renderizando información a la página, los usuarios deberían tener una forma de interactuar con ella. Dentro de la declaración return del componente, configura una expresión ternaria que implementa la siguiente lógica: cuando la página carga por primera vez, renderiza el botón de envío, buttonOne, a la página. Luego, cuando un usuario ingrese su edad y haga clic en el botón, renderiza un botón diferente basado en la edad. Si un usuario introduce un número menor que 18, renderiza buttonThree. Si un usuario introduce un número mayor o igual a 18, renderiza buttonTwo.
```javascript
const inputStyle = {
  width: 235,
  margin: 5
};

class CheckUserAge extends React.Component {
  constructor(props) {
    super(props);
    this.state = {input: '',userAge: ''}
    this.submit = this.submit.bind(this);
    this.handleChange = this.handleChange.bind(this);
  }
  handleChange(e) {
    this.setState({input: e.target.value,userAge: ''});
  }
  submit() {this.setState(state => ({userAge: state.input}));}
  render() {
    const buttonOne = <button onClick={this.submit}>Submit</button>;
    const buttonTwo = <button>You May Enter</button>;
    const buttonThree = <button>You Shall Not Pass</button>;
    return (
      <div>
        <h3>Enter Your Age to Continue</h3>
        <input
          style={inputStyle}
          type='number'
          value={this.state.input}
          onChange={this.handleChange}
        />
        {this.state.userAge === '' ? buttonOne : (this.state.userAge >= 18 ? buttonTwo : buttonThree)}
      </div>
    );
  }
}
```