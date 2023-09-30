---
title: "Js Reduce"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false

---



# JS Reduce

### Introduction

Reduce is a map method which takes and accumulator (where we accumulate the result) and element (each element in the array). Its a pure function it don’t alter anything out of its scope (the original array will remain same).



```js
let z = [1,2,3,4,5];
// we pass a function which take an accumulator and the element of array
let k = z.reduce((acc,ele) => acc + ele,0); // 15
```



### Using Reduce to reduce an array to an object or map

We are given an array and we want it to reduce to an object or map where the value will be the number of times it occurs in the array.

```js
let z = ["vim", "vscode", "emacs", "vscode", "vscode" , "vim"];
```

We can reduce the array to an object  (we can do the same with map) : 

```js
let k = z.reduce((acc,ele) => {
  if(!acc[ele]) {
    acc[ele] = 1;
  } else {
    acc[ele] = acc[ele] + 1;
  }
  return acc;
},{});

console.log(k) // { vim: 2, vscode: 3, emacs: 1 }
```



### Using Reduce to map & filter over large data sets

Lets take an array which has 1 million numbers and we want to take the even integer and multiply them by 2. We can use filter to get the even numbers and then chain it with map to change the value.



```js
// // let z = ["vim", "vscode", "emacs", "vscode", "vscode" , "vim"];
let ele = [];
for(let i = 0; i < 1000000; i++) {
  ele.push(i);
}
// // with using filter and map;
let k;
console.time('k');
k = ele.filter((ele) => ele%2 == 0).map((ele) => ele*2);
console.timeEnd('k'); // 30 ms 

let z;
console.time("z");
z = ele.reduce((acc,ele) => {
  if(ele%2 === 0) {
    acc.push(ele*2);
  }
  return acc;
}, []);
console.timeEnd("z"); // 19 ms
```



So in cases where we got huge datasets its better to use reduce because we can perform both the filter and map operation in one traversal.

### using optional arguments in reduce

We have other two optional argument in reduce the index and the array itself.

Here is an example where we are using it to calculate mean of the array.

```js

let a = [1,2,3,4,5];

let mean = a.reduce((acc,ele,index,arr) => {
  let sum = acc + ele;
    if(index == arr.length - 1) {
      return sum/(index + 1);
    }
  return sum;
},0);

console.log(mean) // 15/5 = 3;
```



### common mistake while using reduce

If we don’t pass an accumulator reduce will always the the value of first element as the accumulator.

Always define the accumulator.

Always return the accumulator.

### flatten and array in reduce / flatmap

Reduce the all sub-array  present in the array a single array.

> :pencil2:    We use .flat method to flatten the array in it we pass an extra argument for depth

> :pencil:  flatMap is flate + .map() method it flats the array upto 1 depth and 
>
> ```js
> // Taking input as an array A having some elements.
> let A = [1, 2, 3, 4, 5];
>  
> // Mapping with map method.
> b = A.map(x => [x * 3]);
> console.log(b);
> 
> //[ [ 3 ], [ 6 ], [ 9 ], [ 12 ], [ 15 ] ]
>  
> // Mapping and flatting with flatMap() method.
> c = A.flatMap(x => [x * 3]);
> 
> // [ 3, 6, 9, 12, 15 ]
> 
> console.log(c);
> ```



To flatten an array we just concat the subarray to the accumulator empty array.

```js
let a = [[1,2,3],[2,2],[3,7,6]];

let flat = a.reduce((acc,ele) => {
  return acc.concat(ele);
},[]);

console.log(flat);
// [1,2,3,2,2,3,7,6];
```

Using reduce to store the name of each cast present inside the array.

```js
let input = [
  {
    title: "Batman Begins",
    year: 2005,
    cast: [
      "Christian Bale",
      "Michael Caine",
      "Liam Neeson",
      "Katie Holmes",
      "Gary Oldman",
      "Cillian Murphy",
    ],
  },
  {
    title: "The Dark Knight",
    year: 2008,
    cast: [
      "Christian Bale",
      "Heath Ledger",
      "Aaron Eckhart",
      "Michael Caine",
      "Maggie Gyllenhal",
      "Gary Oldman",
      "Morgan Freeman",
    ],
  },
  {
    title: "The Dark Knight Rises",
    year: 2012,
    cast: [
      "Christian Bale",
      "Gary Oldman",
      "Tom Hardy",
      "Joseph Gordon-Levitt",
      "Anne Hathaway",
      "Marion Cotillard",
      "Morgan Freeman",
      "Michael Caine",
    ],
  },
];

let stars = input.reduce(function (acc, value) {
  value.cast.forEach(function (star) {
    if (acc.indexOf(star) === -1) {
      acc.push(star);
    }
  });

  return acc;
}, []);
/* [ 'Christian Bale',
  'Michael Caine',
  'Liam Neeson',
  'Katie Holmes',
  'Gary Oldman',
  'Cillian Murphy',
  'Heath Ledger',
  'Aaron Eckhart',
  'Maggie Gyllenhal',
  'Morgan Freeman',
  'Tom Hardy',
  'Joseph Gordon-Levitt',
  'Anne Hathaway',
  'Marion Cotillard' ] */
```

> We can use `reduceRight` to traverse from right side of the array.

### Piping the functions using reduce

```js
function increment(input) { return input + 1;}
function decrement(input) { return input - 1; }
function double(input) { return input * 2; }
function halve(input) { return input / 2; }

let initial_value = 1;

let pipeline = [
  increment,
  increment,
  increment,
  double,
  increment,
  increment,
  halve
];

let final_value = pipeline.reduce(function(acc, fn) {
  return fn(acc);
}, initial_value);

let reversed = pipeline.reduceRight(function(acc, fn) {
  return fn(acc);
}, initial_value)

console.log("final_value: ", final_value)
console.log("reversed: ", reversed)
```



### Reduce to check for missing data

Here anakin don’t have father and the value is missing 

```js
let luke = {
  name: "luke skywalker",
  jedi: true,
  parents: {
    father: {
      jedi: true
    },
    mother: {
      jedi: false
    }
  }
}

let han = {
  name: "han solo",
  jedi: false,
  parents: {
    father: {
      jedi: false
    },
    mother: {
      jedi: false
    }
  }
}

let anakin = {
  name: "anakin skywalker",
  jedi: true,
  parents: {
    mother: {
      jedi: false
    }
  }
}

let characters = [luke, han, anakin];

function fatherWasJedi(character) {
  let path = "parents.father.jedi";
  return path.split(".").reduce(function(obj, field) {
    if (obj) {
      return obj[field];
    }

    return false;
  }, character);
}

characters.forEach(function(character) {
  console.log(character.name + "'s father was a jedi:", fatherWasJedi(character)) 
});
```



