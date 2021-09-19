# 'this' mystry solved 

//Remember, 'this' keyword is used to re-use a function

// There are 4 rules to identify 'this'

// 01. implicit binding ('this' is the object before the 'dot' in the dot notation)
// 02. explicit binding (using .call(), .apply(), .bind())
// 03. new binding  (new Function)
// 04. window binding 


  /////////////////////////////////////////////////////
 //////////// implicit binding - Example 01 //////////
/////////////////////////////////////////////////////
let sam = {
    name: "Sam",
    age: 34,
    printName() {
        console.log(this.name); // 'this' is the object before the 'dot' in the dot notation
    }
}
sam.printName() // 'this' is the object before the 'dot' in the dot notation which is 'sam'




  //////////////////////////////////////////////////////
 //////////// implicit binding - Example 02 ///////////
//////////////////////////////////////////////////////
let createPrintPlayerNameFunction = function(obj) {
    obj.printPlayerName = function() {
        console.log(this.name); // 'this' is the object before the 'dot' in the dot notation
    }
}

let sakib = {
    name: 'Sakib',
    age: 32
};

let tamim = {
    name: 'Tamim',
    age: 34
};

createPrintPlayerNameFunction(sakib);
createPrintPlayerNameFunction(tamim);

tamim.printPlayerName(); // 'this' is the object before the 'dot' in the dot notation which is 'tamim'
sakib.printPlayerName(); // 'this' is the object before the 'dot' in the dot notation which is 'sakib'


  //////////////////////////////////////////////////////
 //////////// implicit binding - Example 03 ///////////
//////////////////////////////////////////////////////
let person = function (name, age) {
    return {
        name: name,
        age: age,
        printName: function () {
            console.log(this.name); // 'this' is the object before the 'dot' in the dot notation
        }
    };
};

let mushfiq = person('Mushfiq', 32);
mushfiq.printName(); // 'this' is the object before the 'dot' in the dot notation which is 'mushfiq'


  //////////////////////////////////////////////////////
 //////////// implicit binding - Example 04 ///////////
//////////////////////////////////////////////////////
let person2 = function (name, age) {
    return {
        name: name,
        age: age,
        printName: function () {
            console.log(this.name); // 'this' is the object before the 'dot' in the dot notation
        },
        father: {
            name: 'XYZ',
            printName() {
                console.log(this.name);
            }
        },
    };
};

let rafiq = person2('Mushfiq', 32);
rafiq.father.printName(); // 'this' is the object before the 'dot' in the dot notation which is 'rafiq.father'


  //////////////////////////////////////////////////////
 //////////// explicit binding - Example 01 ///////////
//////////////////////////////////////////////////////

// ****** Remember, 'this' keyword is used to re-use a function in different contexts

// we can perform explicit binding using .call(), .apply() and .bind()

function printName(v1, v2, v3) {
    console.log(`${this.name} is ${v1}, ${v2} & ${v3}`);
}
let khalid = {
    name: 'Khalid',
    age: 34,
};

let vertue1 = 'Handsome';
let vertue2 = 'Best Player';
let vertue3 = 'All-rounder';

let vertues = [vertue1, vertue2, vertue3];

// -> -> .call() <- <-
// ".call()" is used to call a function in the context of an object 
// it takes the object as its 1st argument 
// and it takes the next all arguments 
// as the arguments of the function it is calling
// as a comma separated list

// here, "this" is the object - the first argument of .call()
printName.call(khalid, vertue1, vertue2, vertue3);


// -> -> .apply() <- <-
// ".apply()" is used to call a function in the context of an object 
// it takes an object its 1st argument 
// and it takes the next argument as an array
// as the arguments of the function it is calling

// here, "this" is the object - the first argument of .apply()
printName.apply(khalid, vertues); 


// -> -> .bind() <- <-
// it works just the same as 'call()'
// but the difference is:
// it doesn't directly call a function
// but it returns an instance of the function
// in other words, it returns the function
// so, the returned function can be stored in a variable
// later, the variable (function) can be called 
// and it will show side effects

let newFunc = printName.bind(khalid, vertue1, vertue2, vertue3);
newFunc();


// How to find the lost 'this' in a callback?
// In other words, how to call a function in a certain context?


  //////////////////////////////////////////////////////
 //////////// explicit binding - Example 02 ///////////
//////////////////////////////////////////////////////

const js = {
    name: 'JavaScript',
    libraries: ['React', 'Angular', 'Vue'],
    printLibraries: function() {
        this.libraries.forEach(function(library) {
            console.log(`${library} is a library of ${this.name}`);
        }.bind(this));
    }
};
js.printLibraries()

  //////////////////////////////////////////////////////
 //////////// explicit binding - Example 03 ///////////
//////////////////////////////////////////////////////

const js = {
    name: 'JavaScript',
    libraries: ['React', 'Angular', 'Vue'],
    printLibraries: function() {
        this.libraries.forEach(library => {
            console.log(`${library} is a library of ${this.name}`);
        });
    }
};
js.printLibraries()


  //////////////////////////////////////////////////////
 //////////// explicit binding - Example 04 ///////////
//////////////////////////////////////////////////////

const js = {
    name: 'JavaScript',
    libraries: ['React', 'Angular', 'Vue'],
    printLibraries: function() {
        const self = this;
        this.libraries.forEach(function(library) {
            console.log(`${library} is a library of ${self.name}`);
        });
    }
};
js.printLibraries()


  //////////////////////////////////////////////////////
 //////////// new binding - Example 01 ////////////////
//////////////////////////////////////////////////////



function Person(name, age) {
    // let this = Object.create(null);
    this.name = name;
    this.age = age;
    console.log(`${this.name} is ${this.age} years old.`);
    // return this;
}

let fahad = new Person('Fahad', 43);


  //////////////////////////////////////////////////////
 //////////// window binding - Example 01 /////////////
//////////////////////////////////////////////////////

// without 'use strict'
// 'use strict' can be used to prevent the default behaviour
// the behaviour acts so that this === window
// when the function is in the global scope

let showName = function () {
    console.log(this); // window
    console.log(this === window) ; // true
    console.log(this.name); // undefined
};

showName();