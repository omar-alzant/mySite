---
title: "Testing -JS-"
date: 2022-06-08
draft: false
project_tags: ["js"]
status: "js"
weight: 20
summary: "Let’s practice! Using ES6 import statements with Jest."
links:
    external_link:
        text: "Some external link"
        icon: "fas fa-external-link-alt"
        href: "https://www.theodinproject.com/lessons/node-path-javascript-testing-practice"
        weight: 1
    another_link:
        text: "Another github link"
        icon: "fab alt brands fa-github"
        href: "https://github.com/omar-alzant/Jest-1-"
        weight: 2
---


</br>
</br>

## Package using :

In this testing project, we use `Jest`,
For more info and tutorial about Jest & babel,
visit this 
<a href="https://jestjs.io/docs/getting-started#using-babel"> 
  Link
</a>.

***

</br>
</br>

## Steps :

Write tests for the following, and then make the tests pass!

1- A `capitalize` function that takes a string and returns it with the first character capitalized.

2- A `reverseString` function that takes a string and returns it reversed.

3- A `calculator` object that contains functions for the basic operations: `add`, `subtract`, `divide`, and `multiply`. Each of these functions should take two numbers and return the correct calculation.

4- A `caesarCipher` function that takes a string and returns it with each character “shifted”. Read more about how a Caesar cipher works on 
<a href="http://practicalcryptography.com/ciphers/caesar-cipher/">
  this website.
</a>

- Don’t forget to test wrapping from z to a.

- Don’t forget to test keeping the same case.

- Don’t forget to test punctuation!

- For this one, you may want to split the final function into a few smaller functions. One concept of Testing is that you don’t need to explicitly test every function you write… Just the public ones. So in this case you only need tests for the final caesarCipher function. If it works as expected you can rest assured that your smaller helper functions are doing what they’re supposed to.

5- An `analyzeArray` function that takes an array of numbers and returns an object with the following properties: `average`, `min`, `max`, and `length`.

```javascript

const object = analyzeArray([1,8,3,4,2,6]);

object == {
  average: 4,
  min: 1,
  max: 8,
  length: 6
};

```

***

</br>
</br>

The Result :

*** 
***


Code -AnalyzeArray- -JS- :

```javascript

// An analyzeArray function that takes an array of numbers and returns an object with the following properties: average, min, max, and length.

//example : 
// const object = analyzeArray([1,8,3,4,2,6]);

// object == {
//     average: 4,
//     min: 1,
//     max: 8,
//     length: 6
//   };

const analyzeArray = (array)=>{
    let l = array.length,
        sum = array.reduce((t,e)=>{ return t+e },0),
        sorta = array.sort((a,b)=> a>b ? 1 : -1);
        return {
            average: sum/l,
            min: sorta[0], // or Math.min(...array)
            max: sorta.pop(), // or Math.max(...array)
            length: l,
        }
}
export default analyzeArray;


```

***

Code -AnalyzeArray- -test- :

```javascript 

import analyzeArray from '../codes/analyzeArray'

describe('analyzeArray', () => {
    test.skip('test the average:', () => {
      expect(analyzeArray([1,8,3,4,2,6]).average).toEqual(4);
    });
    test('removes multiple values', () => {
      expect(analyzeArray([1,8,3,4,2,6]).min).toEqual(1);
    });
    test.skip('ignores non present values', () => {
      expect(analyzeArray([1,8,3,4,2,6]).max).toEqual(8);
    });
    test.skip('ignores non present values, but still works', () => {
      expect(analyzeArray([1,8,3,4,2,6]).length).toEqual(6);
    });
});

```


***

</br>
</br>

Code -CaeserCipher- -JS- :

```javascript

// http://practicalcryptography.com/ciphers/caesar-cipher/

// plain:  abcdefghijklmnopqrstuvwxyz
// cipher: bcdefghijklmnopqrstuvwxyza

const caeserCipher = (s,shift)=>{
    if(shift === 0) return s;
    
    return  s.replace(/[a-z]/g, (c)=>
            String.fromCharCode(c.charCodeAt(0) + shift));
}

module.exports = caeserCipher;
// console.log(caeserCipher('abcdefg',20));

```

***

Code -CaeserCipher- -test- :

```javascript 

// http://practicalcryptography.com/ciphers/caesar-cipher/
// plain:  abcdefghijklmnopqrstuvwxyz
// cipher: bcdefghijklmnopqrstuvwxyza

import caeserCipher from "../codes/caesarCipher"


test('return the string with shift value : ',()=>{
    expect(caeserCipher('abcdefg',20)).toBe('uvwxyz{')
})

```


***

</br>
</br>


Code -Calculator- -JS- :

```javascript
function calc(type,a,b){
    switch(type){
        case '+' : return a+b;
        case '*' : return a*b;
        case '/' : return a/b;
        case '-' : return a-b; 
    }
}

module.exports = calc;
// console.log(calc('+',4,5))


```

***

Code -Calculator- -test- :

```javascript 

import calc from '../codes/calculator'

test('1 + 2 :',()=>{
    expect(calc('+',1,2)).toBe(3);
})

test('1 * 2 :',()=>{
    expect(calc('*',1,2)).toBe(2);
})

test('1 / 2 :',()=>{
    expect(calc('/',1,2)).toBe(0.5);
})

test('1 - 2 :',()=>{
    expect(calc('-',1,2)).toBe(-1);
})


```


***

</br>
</br>


Code -Capitalize- -JS- :

```javascript

// A capitalize function that takes a string and returns it with the first character capitalized.

  function capitalize(s){
    let lower = s.toLowerCase()
    let first = s.charAt(0).toUpperCase();

             return first+lower.slice(1);
}

module.exports = capitalize;
// console.log(capitalize('sddAAAsa'));

```

***

Code -Capitalize- -test- :

```javascript 
import capitalize from '../codes/capitalize';

test('return upper-case the first capital',()=>{
    expect(capitalize('omAr')).toBe('Omar');
});

```


***

</br>
</br>


Code -Reverse- -JS- :

```javascript

// A reverseString function that takes a string and returns it reversed.

function reverseString(s){
    let arrs = s.split('').reverse();
    
    // console.log(arrs.join(''));
    return arrs.join('');
}

    export default reverseString;
// reverseString('ad adki koifd')

```

***

Code -Reverse- -test- :

```javascript 

import reverseString from '../codes/reverseString'

test('return the reverse of this string: ',()=>{
    expect(reverseString('ad adki koifd')).toBe('dfiok ikda da')
});

```


***

</br>
</br>

