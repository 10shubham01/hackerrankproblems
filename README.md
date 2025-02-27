# **5 DESIGN PATTERN USED IN JAVASCRIPT**

### DESIGN PATTERN

A general solution to common software design problems. Like a Blueprint or Tamplet that can be modify to solve a particular problem.

### Categories

1. Creational
   - Factory Pattern
   - Singleton Pattern
2. Behavioral
   - Strategyg Pattern
   - Observer Pattern
3. Structural
   - Proxy Pattern
  
  
  
## CREATIONAL
Patterns are mainly all about providing object creation mechanisms that promote flexibility and usability especially in sitution where need to create many diffrent types of many diffrent objects. 

* #### FACTORY PATTERN 

The factory pattern is a creational design pattern that uses factory methods to create objects — rather than by calling a constructor.

Let's think of the word "Factory" in a real-world sense. A factory is a buliding where things are manufactured. So in the programing sense a factory is just an object that creates or manufacture diffrent objects.

##### Let's just jump into the code !
Let's setup a scenario, let's say there is a software business company having two type of employees.

1: Developers , who write codes for new features
```javascript
function Developer(name)
{
  this.name = name
  this.type = "Developer"
} 
``` 
2:Testers, who write test to makesure these features are working

```javascript
function Tester(name)
{
  this.name = name
  this.type = "Tester"
}
```
And there is Database that keep track of all employees

```javascript
function EmployeeFactory()
{
  this.create = (name, type) => {
    switch(type)
    {
      case 1: // For Developer
        return new Developer(name)
      case 2: // For Tester
        return new Tester(name)
    }
  }
}
```
**create method** is responisble for creating new object.

Print method 

```javascript
function say()
{
  console.log("Hi, I am " + this.name + " and I am a " + this.type)
}

```
Let's create a new instance of factory, and database is going to be an array of employees.

```javascript
const employeeFactory = new EmployeeFactory()
const employees = []

```
Let's start inserting employees into array.
```javascript
employees.push(employeeFactory.create("Shubham", 1))
employees.push(employeeFactory.create("Ajay", 2))
employees.push(employeeFactory.create("Rahul", 1))
employees.push(employeeFactory.create("jhon", 1))
employees.push(employeeFactory.create("Patrick", 2))

```
Let's loop through all of the employees .

```javascript
employees.forEach( emp => {
  say.call(emp)

```
That's how a factory works, its a clean impleation of creating many diffrent types of objects.

* #### SINGLETON PATTERN 
Singleton pattern comes under the **Creational Pattern**, and its comes in handy when there is a requirment of limit the number of instaces of an object to at most one.

The Singleton pattern allows you to limit the number of instances of a particular object to one. This single instance is called the singleton. Singletons reduce the need for global variables which is particularly important in JavaScript because it limits namespace pollution and associated risk of name collisions.

##### Let's just jump into the code !
Let's setup a scenario, let's write a programe that manage the processes having two main component.

1:Process
```javascript
function Process(state)
{
this.state=state
}
```
2:Process Manger inside a function expression
```javascript
const Sinleton=(function(){

    function ProcessManger() {
        this.numProcess = 0
    }

    let pManager

    function createProcessManager() {

        pManger = new ProcessManager()

        return pManger
    }
    return {

        getProcessManager: () => {

            if (!Pmanager)
                pManager = createProcessManager()
            return pManager
        }
    }
})
const processManager=Singleton.getProcessManager();
const processManager2=Singleton.getProcessManager();
console.log(processManager===processManager2)
```
It will print true as output

---
<br>

## BEHAVIORAL 
In software engineering, behavioral design patterns are design patterns that identify common communication patterns among objects. By doing so, these patterns increase flexibility in carrying out communication.

* #### STRATEGY PATTERN
The Strategy pattern is a behavioral design pattern that enables you to define a group (or family) of closely-related algorithms (known as strategies). The strategy pattern allows you to swap strategies in and out for each other as needed at runtime.

##### Let's just jump into the code !
Let's write a programe that gives diffrent some shipping calculations like FedEx, USPS and UPS gonna calculate some shipping cost.

1:FedEx
```javascript 
function Fedex(pkg)
{
  this.calculate = () =>
  {
    // Fedex calculations ...
    return 2.45
  }
}
```
2:UPS
```javascript
function UPS(pkg)
{
  this.calculate = () =>
  {
    // UPS calculations ...
    return 1.56
  }
}
```
3:USP
```javascript
function USPS(pkg)
{
  this.calculate = () =>
  {
    // USPS calculations ...
    return 4.5
  }
}
```
4: Create instances of these
```javascript
const fedex = new Fedex()
const ups = new UPS()
const usps = new USPS()
const pkg = { from: "Alabama", to: "Georgia", weight: 1.56 } 
```
5:Create object constructor called Shippng and it's instances
```javascript
function Shipping()
{
  this.company = ''
  this.setStrategy = company =>
  {
    this.company = company
  }
  this.calculate = pkg => {
    return this.company.calculate(pkg)
  }
}

const shipping = new Shipping()
```
6:Calculate using Shipping
```javascript
shipping.setStrategy(fedex)
console.log("Fedex: " + shipping.calculate(pkg))

shipping.setStrategy(ups)
console.log("UPS: " + shipping.calculate(pkg))

shipping.setStrategy(usps)
console.log("USPS: " + shipping.calculate(pkg))

```

* #### OBSERVER PATTERN 
The Observer pattern is a design pattern that offers a subscription model in which objects (known as 'observers') can subscribe to an event (known as a 'subject') and get notified when the event occurs (or when the subject sends a signal). This pattern is the cornerstone of event driven programming.

##### Let's just jump into the code !
1: Subjejct that keep track of of all the observer

```javascript
function Subject()
{
  this.observers = [] // array of observer functions
}

```
2:Adding some methods to subject
```javascript
Subject.prototype = {
  subscribe: function(fn)
  {
    this.observers.push(fn)
  },
  unsubscribe: function(fnToRemove)
  {
    this.observers = this.observers.filter( fn => {
      if(fn != fnToRemove)
        return fn
    })
  },
  fire: function() // for trigger
  {
    this.observers.forEach( fn => {
      fn.call()
    })
  }
}

```
3:let's test this out
```javascript
const subject = new Subject()

function Observer1()
{
  console.log("Observer 1 Firing!")
}

function Observer2()
{
  console.log("Observer 2 Firing!")
}

subject.subscribe(Observer1)
subject.subscribe(Observer2)
subject.fire() 

subject.unsubscribe(Observer1)
subject.fire()

```
---
<br>

## STRUCTURAL

Structural patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient. Allows objects with incompatible interfaces to collaborate.

* #### PROXY PATTERN
A proxy object is an object that acts as an interface (or placeholder) for something else. The proxy could be an interface to anything: an API, a network connection, a large object in memory, or some other resource that is expensive or impossible to duplicate.

A proxy is a 'stand-in' object that is used to access the 'real' object behind the scenes. In the proxy, extra functionality can be provided, for example caching when operations on the real object are resource intensive, or checking preconditions before operations on the real object are invoked.

##### Let's just jump into the code !
let's write a program that displays values for diffrent crypto currencies, but inorder to get these values we need to make request to some external API.

1:Building API

```javascript 
// External API Service
function CryptocurrencyAPI()
{
  this.getValue = function(coin)
  {
    console.log("Calling External API...")
    switch(coin)
    {
      case "Bitcoin":
        return "$8,500"
      case "Litecoin":
        return "$50"
      case "Ethereum":
        return "$175"
       default:
        return "NA"
    }
  }
}

```
2: Calling API Directly
```javascript
const api = new CryptocurrencyAPI()
console.log("----------Without Proxy----------")
console.log(api.getValue("Bitcoin"))
console.log(api.getValue("Litecoin"))
console.log(api.getValue("Ethereum"))
console.log(api.getValue("Bitcoin"))
console.log(api.getValue("Litecoin"))
console.log(api.getValue("Ethereum"))
```
3:Creating Proxy
```javascript
function CryptocurrencyProxy()
{
  this.api = new CryptocurrencyAPI()
  this.cache = {}

  this.getValue = function(coin)
  {
    if(this.cache[coin] == null)
    {
      this.cache[coin] = this.api.getValue(coin)
    }
    return this.cache[coin]
  }
}

```
4: Calling API with Proxy
```javascript
console.log("----------With Proxy----------")
const proxy = new CryptocurrencyProxy()
console.log(proxy.getValue("Bitcoin"))
console.log(proxy.getValue("Litecoin"))
console.log(proxy.getValue("Ethereum"))
console.log(proxy.getValue("Bitcoin"))
console.log(proxy.getValue("Litecoin"))
console.log(proxy.getValue("Ethereum"))

```
---
Reference links
https://www.youtube.com/channel/UCV4AXpDSxschk8I0sCl8JXw

https://github.com/pkellz
