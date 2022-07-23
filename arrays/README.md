# Arrays


## 1- Introduction

Arrays or as referred to as **lists** are data structures that store data in memory **sequentially** in **contiguous** **order**. Therefore, they have **a small memory footprint**. Arrays are the best choice when it comes to storing data in order and iterating through them. Arrays are great for lookup, push and pop, because they have `O(1)`

## 2 - Big O for array operations:

- lookup → `O(1)`
- Insert →  unshift `O(n)` /  push `O(1)`
- Delete → shift `O(n)` / pop `O(1)`
- Searching → `O(n)`

***Example***: 

```jsx
const letters = ['a', 'b', 'c', 'd']

const firstL = letters[0] // Lookup a specific index => O(1)
letters.push('e') // Push to the end of array => O(1)
letters.pop() // Delete last element of array => O(1)
letters.unshift('x') // Insert at the start of array  => O(n)
letters.splice(2, 0 , 'z') // Insert at a specific index => O(n)
```

## 3 - Static vs Dynamic arrays:

3.1 - Javascript uses dynamic arrays. Even when your array does fill up that extra space you don’t need to do anything. Javascript under the hood will **find space in memory**, **allocate double the amount** of memory you need, store your **original values** as well as **the new values,** and **copy over the values**. [Read more](https://medium.com/@rodriguezlf4/static-vs-dynamic-arrays-javascript-beauty-f226e153cbc9)

### 3.2 - Static array:

an array that allocates at ( **compile-time** ) a **fixed amount of memory** to be used for storing the array’s values on **the stack**. Which means no space to add any new values to the same array.

### 3.3 - Dynamic array:

an array that allocates at ( **run-time )** **double the amount of memory** needed to store the array’s values and the memory is allocated from **the heap.**

## 4 - Implementing an array:

Check the link below to run the code example:  

[Array implementation example](https://replit.com/@Sob7i/Array-implementation-example#index.js:37:2)

```jsx
function shiftIndexBackward(data, length) {
  for (let i = length - 1; i >= 0; i--) {
    data[i + 1] = data[i]
  }
}

function shiftIndexForward(data, length) {
  for (let i = 0; i <= length - 1; i++) {
    data[i] = data[i + 1]
  }
}

class MyArray {
  constructor(data) {
    this.length = 0
    this.data = data || {}
  }

  // O(1)
  get(index) {
    if (index === undefined) throw new Error('argument was expected')
    return this.data[index]
  }
  // O(1)
  push(elem) {
    if (elem === undefined) throw new Error('argument was expected')
    this.data[this.length] = elem
    this.length++
    return this.data[this.length]
  }
  // O(1)
  pop() {
    const lastElem = this.data[this.length - 1]
    delete this.data[this.length - 1]
    this.length--
    return lastElem
  }
  // O(n)
  unshift(elem) {
    if (elem === undefined) throw new Error('argument was expected')
    shiftIndexBackward(this.data, this.length)
    this.data[0] = elem
    this.length++
  }
  // O(n)
  shift() {
    delete this.data[0]
    shiftIndexForward(this.data, this.length)
    delete this.data[this.length - 1]
    this.length--
  }
  // O(n)
  map(cb) {
    if (!cb) throw new Error('argument was expected')
    for (let i = 0; i < this.length; i++) {
      cb(this.data[i], i)
    }
    return this.data
  }
}

```

## 5 - Strings and Arrays:

Strings can actually be treated as **arrays of characters.** 

***Examples***: 

```jsx
function reverse(string) {
  if(typeof string !== 'string' || !string instanceof String)
  throw new Error('Input must be string')
  return Array.from(string).reverse().join('')
}

const reverse2 = (string) => [...string].reverse().join('')

const reverse3 = (string) => string.split('').reverse().join('')

```

***Excercise***: Merge two sorted arrays.

```jsx
function mergeSortedArrays(arr1, arr2) {
  return [...arr1, ...arr2].sort()
}

const arr1 = [1, 4, 7]
const arr2 = [3, 6, 8]

const sorted = mergeSortedArrays(arr1, arr2)
console.log(sorted) // [ 1, 3, 4, 6, 7, 8 ]
```

## 6- Notes: TO BE CONTINUED...

## 7- Why Arrays?

- Arrays have **O(1) random access** but are really **expensive** to **add** stuff onto or **remove** stuff from.
- You need **indexed/random access** to elements.
- You know the **number** of elements in the array ahead of time so that you can allocate the correct amount of memory for the array.