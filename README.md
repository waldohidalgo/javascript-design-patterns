# JavaScript: Patterns

Repositorio que contiene mi resumen del curso [JavaScript: Patterns](https://www.linkedin.com/learning/javascript-patterns-2) dado en Linkedin Learning. He complementado el curso con el siguiente recurso: [patterns.dev](https://www.patterns.dev/)

## Tabla de Contenidos

- [JavaScript: Patterns](#javascript-patterns)
  - [Tabla de Contenidos](#tabla-de-contenidos)
  - [Certificado](#certificado)
  - [Design Pattern](#design-pattern)
    - [1-Creational Patterns](#1-creational-patterns)
      - [1.1-Class design Pattern](#11-class-design-pattern)
      - [1.2-Constructor Pattern](#12-constructor-pattern)
      - [1.3-Singleton Pattern](#13-singleton-pattern)
      - [1.4-Factory Pattern](#14-factory-pattern)
      - [1.5-Abstract Factory Pattern](#15-abstract-factory-pattern)
    - [2-Structural Patterns](#2-structural-patterns)
      - [2.1-Module Pattern](#21-module-pattern)
      - [2.2-Mixins Pattern](#22-mixins-pattern)
      - [2.3-Facade Pattern](#23-facade-pattern)
      - [2.4-Flyweight Pattern](#24-flyweight-pattern)
      - [2.5-Decorator Pattern](#25-decorator-pattern)
      - [2.6-MVC (Model, View, Controller) Pattern](#26-mvc-model-view-controller-pattern)
      - [2.7-MVP (Model, View, Presenter) Pattern](#27-mvp-model-view-presenter-pattern)
      - [2.8-MVVM (Model, View, ViewModel) Pattern](#28-mvvm-model-view-viewmodel-pattern)
    - [3-Behavioral Patterns](#3-behavioral-patterns)
      - [3.1-Observer Pattern](#31-observer-pattern)
      - [3.2-State Pattern](#32-state-pattern)
      - [3.3-Chain of Responsability Pattern](#33-chain-of-responsability-pattern)
      - [3.4-Iterator Pattern](#34-iterator-pattern)
      - [3.5-Strategy Pattern](#35-strategy-pattern)
      - [3.6-Memento Pattern](#36-memento-pattern)
      - [3.7-Mediator Pattern](#37-mediator-pattern)
      - [3.8-Command Pattern](#38-command-pattern)

## Certificado

![Certificado](./certificate.webp)

## Design Pattern

### 1-Creational Patterns

Enfocados en el control del proceso de creación de objetos

#### 1.1-Class design Pattern

```js
class Car {
  constructor(doors, engine, color) {
    this.doors = doors;
    this.engine = engine;
    this.color = color;
  }
}

const civic = new Car(4, "V6", "grey");

console.log(civic);
```

#### 1.2-Constructor Pattern

Definición:

> Patrón que se utiliza para crear objetos en JavaScript. Se usa una función constructor para inicializar el objeto.

```js
class Car {
  constructor(doors, engine, color) {
    this.doors = doors;
    this.engine = engine;
    this.color = color;
  }
}

class SUV extends Car {
  constructor(doors, engine, color) {
    super(doors, engine, color);
    this.wheels = 4;
  }
}

const civic = new Car(4, "V6", "grey");
const cx5 = new SUV(4, "V8", "red");

console.log(civic);
console.log(cx5);
```

#### 1.3-Singleton Pattern

Definición:

> Este patrón de diseño asegura que una clase tenga solo una instancia y proporciona un punto global de acceso a ella

```js
let instance = null;

class Car {
  constructor(doors, engine, color) {
    if (!instance) {
      this.doors = doors;
      this.engine = engine;
      this.color = color;
      instance = this;
    } else {
      return instance;
    }
  }
}
```

#### 1.4-Factory Pattern

Definición:

> Define una interfaz para crear objetos, pero permite a las subclases decidir qué clase instanciar. En este patrón, una función o método se encarga de crear el objeto y devolverlo.

```js
class Car {
  constructor(doors, engine, color) {
    this.doors = doors;
    this.engine = engine;
    this.color = color;
  }
}

class CarFactory {
  createCar(type) {
    switch (type) {
      case "civic":
        return new Car(4, "V6", "grey");
      case "honda":
        return new Car(2, "V8", "red");
    }
  }
}

const factory = new CarFactory();
const myHonda = factory.createCar("honda");
```

#### 1.5-Abstract Factory Pattern

Definición:

> Proporciona una interfaz para crear familias de objetos relacionados o dependientes sin especificar sus clases concretas. Este patrón es útil cuando se deben crear diferentes objetos relacionados y el proceso de creación debe ser independiente de la implementación concreta.

```js
class Car {
  constructor(doors, engine, color) {
    this.doors = doors;
    this.engine = engine;
    this.color = color;
  }
}

class CarFactory {
  createCar(type) {
    switch (type) {
      case "civic":
        return new Car(4, "V6", "grey");
      case "honda":
        return new Car(2, "V8", "red");
    }
  }
}

class SUV {
  constructor(doors, engine, color) {
    this.doors = doors;
    this.engine = engine;
    this.color = color;
  }
}

class SuvFactory {
  createCar(type) {
    switch (type) {
      case "cx5":
        return new Car(4, "V6", "grey");
      case "sante fe":
        return new Car(2, "V8", "red");
    }
  }
}

const carFactory = new CarFactory();
const suvFactory = new SuvFactory();

const autoManufacturer = (type, model) => {
  switch (type) {
    case "car":
      return carFactory.createCar(model);
    case "suv":
      return suvFactory.createCar(model);
  }
};

const cx5 = autoManufacturer("suv", "cx5");

console.log(cx5);
```

### 2-Structural Patterns

Enfocados en la organización del código

#### 2.1-Module Pattern

Separación del código en piezas más pequeñas de alcance propio al módulo

#### 2.2-Mixins Pattern

Definición:

> Agregar funcionalidades a objetos o clases sin utilizar herencia.

```js
class Car {
  constructor(doors, engine, color) {
    this.doors = doors;
    this.engine = engine;
    this.color = color;
  }
}

class CarFactory {
  createCar(type) {
    switch (type) {
      case "civic":
        return new Car(4, "V6", "grey");
      case "honda":
        return new Car(2, "V8", "red");
    }
  }
}

class SUV {
  constructor(doors, engine, color) {
    this.doors = doors;
    this.engine = engine;
    this.color = color;
  }
}

class SuvFactory {
  createCar(type) {
    switch (type) {
      case "cx5":
        return new Car(4, "V6", "grey");
      case "sante fe":
        return new Car(2, "V8", "red");
    }
  }
}

let carMixin = {
  revEngine() {
    console.log(`The ${this.engine} engine is doing Vroom Vroom!`);
  },
};

const carFactory = new CarFactory();
const suvFactory = new SuvFactory();

const autoManufacturer = (type, model) => {
  switch (type) {
    case "car":
      return carFactory.createCar(model);
    case "suv":
      return suvFactory.createCar(model);
  }
};

Object.assign(Car.prototype, carMixin);

const honda = autoManufacturer("car", "honda");

honda.revEngine();
```

#### 2.3-Facade Pattern

Definición:

> Ocultar complejidad mediante la creación de una "fachada" detrás de la cual esta el código de mayor complejidad en otras palabras proporciona una interfaz simplificada para un conjunto de interfaces en un subsistema complejo.

#### 2.4-Flyweight Pattern

Definición:

> Método para evitar recrear el mismo objeto dos veces de modo de minifizar el uso de memoria

Ejemplo tomado de [https://www.patterns.dev/](https://www.patterns.dev/)

```js
class Book {
  constructor(title, author, isbn) {
    this.title = title;
    this.author = author;
    this.isbn = isbn;
  }
}

const books = new Map();
const bookList = [];

const addBook = (title, author, isbn, availability, sales) => {
  const book = {
    ...createBook(title, author, isbn),
    sales,
    availability,
    isbn,
  };

  bookList.push(book);
  return book;
};

const createBook = (title, author, isbn) => {
  const existingBook = books.has(isbn);

  if (existingBook) {
    return books.get(isbn);
  }

  const book = new Book(title, author, isbn);
  books.set(isbn, book);

  return book;
};

addBook("Harry Potter", "JK Rowling", "AB123", false, 100);
addBook("Harry Potter", "JK Rowling", "AB123", true, 50);
addBook("To Kill a Mockingbird", "Harper Lee", "CD345", true, 10);
addBook("To Kill a Mockingbird", "Harper Lee", "CD345", false, 20);
addBook("The Great Gatsby", "F. Scott Fitzgerald", "EF567", false, 20);

console.log("Total amount of copies: ", bookList.length);
console.log("Total amount of books: ", books.size);
```

#### 2.5-Decorator Pattern

Definición:

> Patrón que permite añadir funcionalidad a un objeto de manera dinámica sin alterar su estructura. Se crea a partir de un wrapper que envuelve al objeto inicial añadiendo nuevas funcionalidades.

```js
function sendMessage(message) {
  console.log(`Sending message: ${message}`);
}

function withTimestamp(fn) {
  return function (message) {
    const timestamp = new Date().toISOString();
    fn(`[${timestamp}] ${message}`);
  };
}
const sendMessageWithTimestamp = withTimestamp(sendMessage);
sendMessageWithTimestamp("Hello, World!");
```

#### 2.6-MVC (Model, View, Controller) Pattern

Definición:

> Define la organización de módulos en tres categorías: el Model es donde reside la data y lógica de negocio, la View contiene los módulos relacionados con la visualización de la data y Controller corresponde a los módulos que contienen la lógica de la aplicación. La View con el Model estan estrechamente relacionadas tal que las Views obtienen la data desde el Modelo. Las entradas en las View son manejadas por el controlador el cual actualiza el modelo.

#### 2.7-MVP (Model, View, Presenter) Pattern

Definición:

> Semejante al MVC pero se diferencia en que las Views solo tienen acceso a los Controllers (quienes ahora se llaman Presentador), siendo estos quienes interactuan con el Modelo, obtienen la data y la pasan a las Views. En este caso el Presentador posee dos funciones: manejar las entradas desde las Views y actualizar las Views con la data del Modelo.

#### 2.8-MVVM (Model, View, ViewModel) Pattern

Definición:

> Se compone de una View encargada de presentar la data e interactuar con el usuario.Dicha View se relaciona con la ViewModel la cual maneja la interacción entre la View y el Modelo. La relación de la View con la ViewModel es poder medio del enlace de datos (data-binding) permitiendo que los cambios en el ViewModel se reflejen automáticamente en la View y viceversa.

### 3-Behavioral Patterns

Enfocado en la comunicación entre objetos

#### 3.1-Observer Pattern

```js
class Car {
  constructor(gas) {
    this.gas = gas;
    this.actions = [];
  }

  setGasLevel(val) {
    this.gas = val;
    this.notifyAll();
  }

  register(observer) {
    this.actions.push(observer);
  }

  unregister(observer) {
    this.actions.remove.filter(function (el) {
      return el !== observer;
    });
  }

  notifyAll() {
    return this.actions.forEach(
      function (el) {
        el.update(this);
      }.bind(this)
    );
  }
}

class consumption {
  update(car) {
    car.gas = car.gas + 1;
  }
}
```

#### 3.2-State Pattern

Definición:

> Patrón que permite a un objeto cambiar su comportamiento cuando su estado interno cambia

#### 3.3-Chain of Responsability Pattern

Definición:

> Patrón que permite que un objeto pase una request a lo largo de una cadena de handlers hasta que uno de ellos la maneje. Cada handler en la cadena tiene la oportunidad de procesar la solicitud o de pasarla al siguiente handler en la cadena.

```js
class Handler {
  constructor(successor = null) {
    this.successor = successor;
  }

  handleRequest(request) {
    if (this.successor) {
      this.successor.handleRequest(request);
    }
  }
}

class ConcreteHandlerA extends Handler {
  handleRequest(request) {
    if (request === "A") {
      console.log("ConcreteHandlerA handled the request.");
    } else {
      super.handleRequest(request);
    }
  }
}
class ConcreteHandlerB extends Handler {
  handleRequest(request) {
    if (request === "B") {
      console.log("ConcreteHandlerB handled the request.");
    } else {
      super.handleRequest(request);
    }
  }
}

class ConcreteHandlerC extends Handler {
  handleRequest(request) {
    if (request === "C") {
      console.log("ConcreteHandlerC handled the request.");
    } else {
      super.handleRequest(request);
    }
  }
}

const handlerC = new ConcreteHandlerC();
const handlerB = new ConcreteHandlerB(handlerC);
const handlerA = new ConcreteHandlerA(handlerB);

handlerA.handleRequest("A"); // ConcreteHandlerA handled the request.
handlerA.handleRequest("B"); // ConcreteHandlerB handled the request.
handlerA.handleRequest("C"); // ConcreteHandlerC handled the request.
handlerA.handleRequest("D"); // (No handler processes 'D')
```

#### 3.4-Iterator Pattern

Definición:

> Patrón que permite recorrer los elementos de una colección sin exponer su representación subyacente. Este patrón proporciona una forma uniforme de acceder a los elementos de una colección de manera secuencial.

Componentes del Iterator Pattern

1-**Iterador (Iterator)**: Define una interfaz para acceder y recorrer los elementos de una colección.

2-**Iterador Concreto (Concrete Iterator)**: Implementa la interfaz del Iterador y mantiene el seguimiento de la posición actual en la colección.

3-**Colección (Collection)**: Define una interfaz para crear un iterador.

4-**Colección Concreta (Concrete Collection)**: Implementa la interfaz de la colección y devuelve una instancia de un iterador concreto.

```js
// Interfaz del Iterador
class Iterator {
  next() {
    throw new Error("Method next() must be implemented.");
  }

  hasNext() {
    throw new Error("Method hasNext() must be implemented.");
  }
}

// Iterador Concreto
class ConcreteIterator extends Iterator {
  constructor(collection) {
    super();
    this.collection = collection;
    this.position = 0;
  }

  next() {
    if (this.hasNext()) {
      return this.collection[this.position++];
    }
    return null;
  }

  hasNext() {
    return this.position < this.collection.length;
  }
}

// Colección
class Collection {
  createIterator() {
    throw new Error("Method createIterator() must be implemented.");
  }
}

// Colección Concreta
class ConcreteCollection extends Collection {
  constructor(items) {
    super();
    this.items = items;
  }

  createIterator() {
    return new ConcreteIterator(this.items);
  }
}

// Uso del patrón Iterator
const collection = new ConcreteCollection(["item1", "item2", "item3"]);
const iterator = collection.createIterator();

while (iterator.hasNext()) {
  console.log(iterator.next()); // item1, item2, item3
}
```

#### 3.5-Strategy Pattern

Definición:

> Patrón que permite definir una familia de algoritmos, encapsular cada uno de ellos y hacerlos intercambiables. El patrón de estrategia permite que el algoritmo varíe independientemente de los clientes que lo utilizan. Es útil cuando se tienen múltiples formas de realizar una tarea específica y se desea cambiar el algoritmo usado sin modificar el código del cliente que utiliza estos algoritmos.

Componentes del Strategy Pattern

-**Contexto (Context)**: Mantiene una referencia a una estrategia y delega la ejecución del algoritmo a la estrategia concreta.

-**Estrategia (Strategy)**: Define una interfaz común para todos los algoritmos compatibles.

-**Estrategias Concretas (Concrete Strategies)**: Implementan la interfaz de la estrategia con un algoritmo específico.

```js
// Estrategia
class Strategy {
  execute(a, b) {
    throw new Error("Method execute() must be implemented.");
  }
}

// Estrategia Concreta: Sumar
class AddStrategy extends Strategy {
  execute(a, b) {
    return a + b;
  }
}

// Estrategia Concreta: Restar
class SubtractStrategy extends Strategy {
  execute(a, b) {
    return a - b;
  }
}

// Estrategia Concreta: Multiplicar
class MultiplyStrategy extends Strategy {
  execute(a, b) {
    return a * b;
  }
}

// Contexto
class Context {
  constructor(strategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy) {
    this.strategy = strategy;
  }

  executeStrategy(a, b) {
    return this.strategy.execute(a, b);
  }
}

// Uso del patrón Strategy
const context = new Context(new AddStrategy());
console.log(context.executeStrategy(5, 3)); // 8

context.setStrategy(new SubtractStrategy());
console.log(context.executeStrategy(5, 3)); // 2

context.setStrategy(new MultiplyStrategy());
console.log(context.executeStrategy(5, 3)); // 15
```

#### 3.6-Memento Pattern

Definición:

> Patrón que permite capturar y almacenar el estado interno de un objeto en un momento dado, para poder restaurarlo posteriormente. Es como tomar una "instantánea" de un objeto en un punto específico en el tiempo.

Componentes del Memento Pattern

-**Originador (Originator)**: El objeto cuyo estado interno desea guardarse. Tiene un método para crear un memento que capture su estado actual y otro método para restaurar su estado desde un memento.

-**Memento**: Un objeto que almacena una copia del estado del Originador.

-**Guardían (Caretaker)**: Un objeto que almacena los mementos y los proporciona al Originador cuando sea necesario.

```js
// Clase Memento
class Memento {
  constructor(state) {
    this.state = state;
  }

  getState() {
    return this.state;
  }
}

// Clase Originator
class Originator {
  constructor() {
    this.state = "";
  }

  setState(state) {
    console.log(`Setting state to ${state}`);
    this.state = state;
  }

  getState() {
    return this.state;
  }

  saveStateToMemento() {
    console.log("Saving state to Memento.");
    return new Memento(this.state);
  }

  getStateFromMemento(memento) {
    this.state = memento.getState();
    console.log(`State restored from Memento: ${this.state}`);
  }
}

// Clase Caretaker
class Caretaker {
  constructor() {
    this.mementoList = [];
  }

  add(memento) {
    this.mementoList.push(memento);
  }

  get(index) {
    return this.mementoList[index];
  }
}

// Uso del patrón Memento
const originator = new Originator();
const caretaker = new Caretaker();

originator.setState("State #1");
originator.setState("State #2");
caretaker.add(originator.saveStateToMemento());

originator.setState("State #3");
caretaker.add(originator.saveStateToMemento());

originator.setState("State #4");
console.log(`Current State: ${originator.getState()}`);

originator.getStateFromMemento(caretaker.get(0));
console.log(`First saved State: ${originator.getState()}`);
originator.getStateFromMemento(caretaker.get(1));
console.log(`Second saved State: ${originator.getState()}`);
```

#### 3.7-Mediator Pattern

Definición:

> Este patrón proporciona un ente central que permite la interacción entre objetos en vez de permitir la interacción entre los mismos objetos. En otras palabras, define un objeto que encapsula cómo interactúan un conjunto de objetos.

Componentes del Mediator Pattern

-**Mediador (Mediator)**: Define una interfaz para la comunicación entre los objetos.

-**Mediador Concreto (Concrete Mediator)**: Implementa la interfaz del mediador y coordina la comunicación entre los objetos colegas.

-**Colega (Colleague)**: Representa los objetos que se comunican a través del mediador. Cada colega conoce al mediador y se comunica con otros colegas a través de él.

```js
// Clase Mediador define interfaz
class Mediator {
  notify(sender, event) {
    throw new Error("Method notify() must be implemented.");
  }
}

// Clase Torre de Control (Mediador Concreto)
class ControlTower extends Mediator {
  constructor() {
    super();
    this.airplanes = [];
  }

  addAirplane(airplane) {
    this.airplanes.push(airplane);
    airplane.setMediator(this);
  }

  notify(sender, event) {
    console.log(`ControlTower received event: ${event} from ${sender.name}`);
    this.airplanes.forEach((airplane) => {
      if (airplane !== sender) {
        airplane.receive(event); // notificación a otros aviones
      }
    });
  }
}

// Clase Avión (Colega)
class Airplane {
  constructor(name) {
    this.name = name;
    this.mediator = null;
  }

  setMediator(mediator) {
    this.mediator = mediator;
  }

  send(event) {
    console.log(`${this.name} sends event: ${event}`);
    this.mediator.notify(this, event);
  }

  receive(event) {
    console.log(`${this.name} received event: ${event}`);
  }
}

// Uso del patrón Mediador
const controlTower = new ControlTower();

const airplane1 = new Airplane("Airplane 1");
const airplane2 = new Airplane("Airplane 2");
const airplane3 = new Airplane("Airplane 3");

controlTower.addAirplane(airplane1);
controlTower.addAirplane(airplane2);
controlTower.addAirplane(airplane3);

airplane1.send("Taking off");
airplane2.send("Landing");
```

#### 3.8-Command Pattern

Definición:

> Básicamente, permite desacoplar objetos que ejecutan una cierta tarea desde el objeto que llama al método de ejecución el cual es común

Componentes del Command Pattern

-**Command (Comando)**: Interfaz que declara un método para ejecutar una acción.

-**Concrete Command (Comando Concreto)**: Implementa la interfaz Command y define la asociación entre un receptor y una acción.

-**Receiver (Receptor)**: Clase que realiza las acciones específicas asociadas con las solicitudes.

-**Invoker (Invocador)**: Clase que solicita la ejecución del comando.

-**Client (Cliente)**: Clase que crea el comando y lo configura con el receptor

```js
// Interfaz Command
class Command {
  execute() {
    throw new Error("Method execute() must be implemented.");
  }

  undo() {
    throw new Error("Method undo() must be implemented.");
  }
}

// Receiver: Dispositivo de Luz
class Light {
  on() {
    console.log("Light is ON");
  }

  off() {
    console.log("Light is OFF");
  }
}

// Concrete Command: Encender la luz
class LightOnCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.on();
  }

  undo() {
    this.light.off();
  }
}

// Concrete Command: Apagar la luz
class LightOffCommand extends Command {
  constructor(light) {
    super();
    this.light = light;
  }

  execute() {
    this.light.off();
  }

  undo() {
    this.light.on();
  }
}

// Invoker: Control Remoto
class RemoteControl {
  setCommand(command) {
    this.command = command;
  }

  pressButton() {
    this.command.execute();
  }

  pressUndo() {
    this.command.undo();
  }
}

// Client: Uso del patrón Command
const light = new Light();
const lightOnCommand = new LightOnCommand(light);
const lightOffCommand = new LightOffCommand(light);

const remote = new RemoteControl();

remote.setCommand(lightOnCommand);
remote.pressButton(); // Light is ON
remote.pressUndo(); // Light is OFF

remote.setCommand(lightOffCommand);
remote.pressButton(); // Light is OFF
remote.pressUndo(); // Light is ON
```
