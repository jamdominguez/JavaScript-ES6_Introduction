# JavaScript-ES6_Introduction
Introduction to ES6 using Node and Webpack.
Reference to Udemy course: https://www.udemy.com/essentials-in-javascript-es6/

## Table of contents
- [JavaScript-ES6_Introduction](#JavaScript-ES6Introduction)
  - [Table of contents](#Table-of-contents)
  - [What is new in ES6?](#What-is-new-in-ES6)
  - [Tools](#Tools)
- [1. Project Configuration](#1-Project-Configuration)
  - [1.1. Set up Project Webpack 4](#11-Set-up-Project-Webpack-4)
  - [1.2. Configure Webpack and Development Server](#12-Configure-Webpack-and-Development-Server)
  - [1.3. Set up Babel with Webpack](#13-Set-up-Babel-with-Webpack)
- [2. Coding New ES6 Syntax](#2-Coding-New-ES6-Syntax)
  - [2.1. Declare variables and scope](#21-Declare-variables-and-scope)
  - [2.2. Declare constants](#22-Declare-constants)
  - [2.3. Template Literals/Strings](#23-Template-LiteralsStrings)
  - [3 Operating and Destructuring](#3-Operating-and-Destructuring)
    - [3.1. Destructuring assignament - Arrays](#31-Destructuring-assignament---Arrays)
    - [3.2. Destructuring assignament - Objects](#32-Destructuring-assignament---Objects)
- [4. Functions and Methods](#4-Functions-and-Methods)
  - [4.1. Arrow Functions](#41-Arrow-Functions)
  - [4.2. Arrow Function ignoring **this**](#42-Arrow-Function-ignoring-this)
  - [4.3. Map Method](#43-Map-Method)

## What is new in ES6?
- Syntax and features
- Classes, modules, array and object manipulation

## Tools
- Node: Install or use portable version setting Node path into "path" environment variable. With node we can use node package manager (npm) to installa dependencies.
  ``` command
  node -v    ..... To show the Node version
  npm -v     ..... To show the Node version
  npm i npm  ..... To show the Node version
  ```

- Babel: A transpiler reads code written in one language and produces the equivalent code in another. Browsers only currently have widespread support of older JS. Transpiler convert advanced TypeScript and CoffeScript code back into the original JS. Transpiles ES6 back into the supported pre ES6 JS. Babel is a JavaScript compiler.
 - Webpack: It is a npm, It allows us to run in an environment that hosts VAP. The benefist:
    - It bundles modules into one .js file    
    - Comes with a dev-server


# 1. Project Configuration
## 1.1. Set up Project Webpack 4
- The package.json vs package-lock.json
    ``` command
    npm init -y ..... Creates the package.json (initialize the project)
    npm install ..... Install all dependencies defined into package.json file
    ```
- The package-lock.json file stores the project dependencies.
- For install webpack dependencies (webpack and webpack command line), execute the next command:
    ``` command
    npm i webpack@4.12.0 webpack-cli@3.0.3 --save--dev ..... install webpack and webpack-cli and save them for develop environment  
    ```
- For execute scripts into package.json use npm command like "npm run start" or "npm run build". This command will execute the commands relationship with the script name "start" or "build".
    ```` command
    npm run start ..... execute "webpack --mode development", this command will create a "dist" folder and main.js file
    npm run build ..... will do the same that start, but the main.js file will be minimized because the mode will be "production"
    ````
## 1.2. Configure Webpack and Development Server
Webpack let export the application like bundle. For it is necessary configure the "webpack.config.js" file. to define the module export. <br>
With the bundle funcionality will get the "build" folder with "bundle.js" and not need anymore the "dist" folder.
Is necessary install a webpack server to test the application. For this:
```` command
npm i webpack-dev-server@3.1.4 --save-dev ..... to install a webpack development server
````
Now is necessary change the "start" script inside package.json to "webpack-dev-server --module development".
Is necessary too add a new key "devServer" into webpack.config.js to define the devlopment server features.
After add the new key, when the command "npm run start" application will be deployed and the server will be run.
With the server run, the changes into "index.js" (file into app folder) can be shown inmeidately in the browser.
The package.json will be:
````json
{
  "name": "es6",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "webpack-dev-server --mode development",
    "buildDev": "webpack --mode development",
    "buildProd": "webpack --mode production"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "webpack": "^4.12.0",
    "webpack-cli": "^3.0.3"
  },
  "devDependencies": {
    "babel-core": "^6.26.3",
    "babel-loader": "^7.1.4",
    "babel-preset-env": "^1.7.0",
    "webpack-dev-server": "^3.1.4"
  }
}
````

## 1.3. Set up Babel with Webpack
The main job of Babel is transfer all moder javascript ES6 to ES5. ES5 is fully supported on all browsers. <br>
Is necessary add three new dependencies related to configuring Babel:
````command
npm i babel-core@6.26.3 babel-loader@7.1.4 babel-preset-env@1.7.0 --save-dev ..... install the Babel core, loader y preset environment
````
Babel must be configured into "webpack.config.js" file, add a new key for this "module". But is necessary a extra configuration, for this create a new file ".babelrc"

# 2. Coding New ES6 Syntax
## 2.1. Declare variables and scope
Exist 2 ways for declare variables in JavaScript:
- Using "var" for function scope
- Using "let" for block scope
In ES6 "let" keyword is used instead of "var". The "var" keyword can be used for global application variables.
````javascript
var name = 'John Snow';
let a = 'hello';
console.log('Before block: '+a+' '+name); //show hello

{
    console.log(a) //a variable doen't exist in this scope (undefined)
    var name = 'Ned Stark';
    let a = 'bye';
    console.log('Inside block: '+a+' '+name); //show bye
    let b = 1000
}

console.log('After block:'+a+' '+name); //show hello
console.log(b); //show a ERROR because the variable let exist only in the block (undefined)
````

## 2.2. Declare constants
In JavaScript a constant is declared with "const" keyword. The constant will be the reference to the variable, it is clarified in array example.
````javascript
const DATA = 2;
console.log('This is a constant: '+DATA)
//DATA = 3*4; //show a ERROR no catcheable, DATA is read-only
const ARRAY = [1,2,3]
console.log(ARRAY);
ARRAY.push(4);
console.log(ARRAY); //the array can be modified but ARRAY constant doesn't have another value (can't be reassigned)
//ARRAY = [1]; //show a ERROR no catcheable, ARRAY is read-only
````

## 2.3. Template Literals/Strings
In ES6 is possible optimized concatenation using templates. It is used like regular expressio, they have surrounding backticks `` with interpolated ${} symbols for variables.
````javascript
var greeting = 'hello';
var name = 'world';
var message_01 = greeting+' '+name;
console.log(message_01);

let message_02 = `${greeting} ${name}`; //ES6 template for literals/strings
console.log(message_02);
````

## 3 Operating and Destructuring
### 3.1. Destructuring assignament - Arrays
ES6 introduces a new way to manipulate arrays and objects.
It is possible include a array into other one using "..." spread operator. It is equivalent to ".concat" instruction in ES5 (use Babel transpiler).
````javascript
//ES6
let first_array = [7,8,9];
let second_array = [6, ...first_array,10];
console.log(second_array);
//Similar code in ES5
var first_array = [7, 8, 9];
var second_array = [6].concat(first_array, [10]);
console.log(second_array);
````
In ES6 use spread operator to pass server params into function. If the array is length minor than functio param, the last params will be undefined, but the lenght is bigger the first array values will be used by params. The next function works with the array component like isolate variables:
````javascript
function print(a,b,c) {
    console.log(a,b,c);
}
let z = [1,2,3];
let y = [9,8];
let w = [4,5,6,7];
print(...z); //show 1 2 3
print(...y); //show 9 8 undefined
print(...w); //show 4 5 6
````

To get any arguments number like array the function can be defined. The next function works with the array componet like array:

````javascript
function print2(...z){
    console.log(z);
}
print2(z); //show [Array(3)]
print2(...z); //show [1,2,3]
print2(1,2,3,4,5,6,7,8); //show [1,2,3,4,5,6,7,8]
print2(1,'hello',true,2); //show [1,"hello",true,2]
````

For destructuring assignament, it is possible generate several variables from array:
````javascript
let heroes = ['Ryu Hayabusa', 'WonderWoman', 'Thor'];
let [ninja, fighter, throw_thunder] = heroes; //3 variables
console.log(ninja, fighter, throw_thunder);
let [human,...goods] = heroes; //1 variable (position 0), 1 array (positions 1 and 2)
console.log(human, goods);
````
### 3.2. Destructuring assignament - Objects
It is possible apply the destructuring assignament to JavaScript Objects:
````javascript
// Before ES6
let wizard = {
    magical: true,
    power: 10
}
let magical = wizard.magical;
let power = wizard.power;
console.log(magical,power);
````
Use several lines to assigne variables is so heavy, with ES6 it is possible assigne variable in only one line using destructuring method:
````javascript
// ES6
let wizard = {
    magical: true,
    power: 10
}
let {magical, power} = wizard;
console.log("Wizard", magical,power);
````
Note that using destructuring assignament with array, in the variables's bunch is used **[]** characters while in the destructuring assignament with objects, in the variables's bunch is used **{}** characters.<br>
In the destructuring with object the name of the variables and the name of the objcet property must be the same to assing the value. It is possible reuse the variables name using a new code block with **()** characters.
````javascript
let warrior = {
    magical: false,
    power: 12
}
let {magical_01, power_01} = warrior;
console.log('Warrior',magical_01,power_01); // show undefined undefined, the variables and object properties has diferrent names

({magical,power} = warrior); //Use () to create new block and can assig the variables
console.log('Warrior',magical,power);
````

# 4. Functions and Methods
## 4.1. Arrow Functions
Arrow functions are anonymous, don't have a named identifier.
It is called an air function
````javascript
function() {...} VS () => {...}
````
````javascript
function boom(){
    console.log('boom()  3...2...1...BOOM!');
}
boom();
const otherBoom = () => {
    console.log('boom()  3...2...1...Other BOOM!');
}
otherBoom();
````
It is usefull when implement business logic with anonymous functions like **setTimeout** or **setInterval** methods.
````javascript
setTimeout(function(){
    console.log('setTimeout  3...2...1...BOOM!');
}, 1000);
setTimeout(() => {
    console.log('setTimeout  3...2...1...BOOM!');
}, 1000);
//
let i = 3;
let myCount = setInterval(function(){
    if (i > 0) {
        console.log(`${i--} ...`);    
    } else {
        console.log('BOOM!');
        clearInterval(myCount);
    } 
}, 1000);

let j = 3;
let myOtherCount = setInterval(() => {
    if (j > 0) {
        console.log(`${j--} ...`);    
    } else {
        console.log('Ohter BOOM!');
        clearInterval(myOtherCount);
    } 
}, 1000);
````

## 4.2. Arrow Function ignoring **this**
Arrow functions do not bind their own **this**. Each function has its own scope and it creates for itselfs a new keyword called this within that scope.<br>
**This** is an object that within the function scope. The function then bind keys and values to the this object.
````javascript
this.a = 10;
const newprint = function() {    
    console.log('this.a',this.a); //show undefined, no property a inside function
}
newprint();

const newarrowPrint = () => {
    console.log('this.a in arrowPrint',this.a); //show 10, aroww function don't have this object in the scope
}
newarrowPrint();
````

## 4.3. Map Method