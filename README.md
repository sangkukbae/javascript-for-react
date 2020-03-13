# javascript-for-react

## [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
```jsx
const greeting = 'Hello'
const subject = 'World'
console.log(`${greeting} ${subject}!`) // Hello World!
// this is the same as:
console.log(greeting + ' ' + subject + '!')
// in React:
function Box({className, ...props}) {
  return <div className={`box ${className}`} {...props} />
}
```

## [Shorthand property names](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015)
```jsx
const a = 'hello'
const b = 42
const c = {d: [true, false]}
console.log({a, b, c})
// this is the same as:
console.log({a: a, b: b, c: c})
// in React:
function Counter({initialCount, step}) {
  const [count, setCount] = useCounter({initialCount, step})
  return <button onClick={setCount}>{count}</button>
}
```

## [Arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

```jsx
const getFive = () => 5
const addFive = a => a + 5
const divide = (a, b) => a / b
// this is the same as:
function getFive() {
  return 5
}
function addFive(a) {
  return a + 5
}
function divide(a, b) {
  return a / b
}
// in React:
function TeddyBearList({teddyBears}) {
  return (
    <ul>
      {teddyBears.map(teddyBear => (
        <li key={teddyBear.id}>
          <span>{teddyBear.name}</span>
        </li>
      ))}
    </ul>
  )
}
```

## [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
```jsx
function makeCalculation({x, y: d, z = 4}) {
  return Math.floor((x + d + z) / 3)
}
// this is the same as
function makeCalculation(obj) {
  const {x, y: d, z = 4} = obj
  return Math.floor((x + d + z) / 3)
}
// which is the same as
function makeCalculation(obj) {
  const x = obj.x
  const d = obj.y
  const z = obj.z === undefined ? 4 : obj.z
  return Math.floor((x + d + z) / 3)
}
// in React:
function UserGitHubImg({username = 'ghost', ...props}) {
  return <img src={`https://github.com/${username}.png`} {...props} />
}
```

## [Parameter defaults](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
```jsx
function add(a, b = 0) {
  return a + b
}
// is the same as
const add = (a, b = 0) => a + b
// is the same as
function add(a, b) {
  b = b === undefined ? 0 : b
  return a + b
}
// in React:
function useLocalStorageState({
  key,
  initialValue,
  serialize = v => v,
  deserialize = v => v,
}) {
  const [state, setState] = React.useState(
    () => deserialize(window.localStorage.getItem(key)) || initialValue,
  )
  const serializedState = serialize(state)
  React.useEffect(() => {
    window.localStorage.setItem(key, serializedState)
  }, [key, serializedState])
  return [state, setState]
}
```

## [Rest](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)/[Spread](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
```jsx
const arr = [5, 6, 8, 4, 9]
Math.max(...arr)
// is the same as
Math.max.apply(null, arr)
const obj1 = {
  a: 'a from obj1',
  b: 'b from obj1',
  c: 'c from obj1',
  d: {
    e: 'e from obj1',
    f: 'f from obj1',
  },
}
const obj2 = {
  b: 'b from obj2',
  c: 'c from obj2',
  d: {
    g: 'g from obj2',
    h: 'g from obj2',
  },
}
console.log({...obj1, ...obj2})
// is the same as
console.log(Object.assign({}, obj1, obj2))
function add(first, ...rest) {
  return rest.reduce((sum, next) => sum + next, first)
}
// is the same as
function add() {
  const first = arguments[0]
  const rest = Array.from(arguments).slice(1)
  return rest.reduce((sum, next) => sum + next, first)
}
// in React:
function Box({className, ...restOfTheProps}) {
  const defaultProps = {
    className: `box ${className}`,
    children: 'Empty box',
  }
  return <div {...defaultProps} {...restOfTheProps} />
}
```
## [Import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)/[Export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export)
```jsx
export default function add(a, b) {
  return a + b
}
/*
 * import add from './add'
 * console.assert(add(3, 2) === 5)
 */
export const foo = 'bar'
/*
 * import {foo} from './foo'
 * console.assert(foo === 'bar')
 */
export function subtract(a, b) {
  return a - b
}
export const now = new Date()
/*
 * import {subtract, now} from './stuff'
 * console.assert(subtract(4, 2) === 2)
 * console.assert(now instanceof Date)
 */
// in React:
import React, {Suspense, Fragment} from 'react'
```

## [Ternaries](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
```jsx
const message = bottle.fullOfSoda
  ? 'The bottle has soda!'
  : 'The bottle may not have soda :-('
// is the same as
let message
if (bottle.fullOfSoda) {
  message = 'The bottle has soda!'
} else {
  message = 'The bottle may not have soda :-('
}
// in React:
function TeddyBearList({teddyBears}) {
  return (
    <React.Fragment>
      {teddyBears.length ? (
        <ul>
          {teddyBears.map(teddyBear => (
            <li key={teddyBear.id}>
              <span>{teddyBear.name}</span>
            </li>
          ))}
        </ul>
      ) : (
        <div>There are no teddy bears. The sadness.</div>
      )}
    </React.Fragment>
  )
}
```

## [Array Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
```jsx
const dogs = [
  {
    id: 'dog-1',
    name: 'Poodle',
    temperament: [
      'Intelligent',
      'Active',
      'Alert',
      'Faithful',
      'Trainable',
      'Instinctual',
    ],
  },
  {
    id: 'dog-2',
    name: 'Bernese Mountain Dog',
    temperament: ['Affectionate', 'Intelligent', 'Loyal', 'Faithful'],
  },
  {
    id: 'dog-3',
    name: 'Labrador Retriever',
    temperament: [
      'Intelligent',
      'Even Tempered',
      'Kind',
      'Agile',
      'Outgoing',
      'Trusting',
      'Gentle',
    ],
  },
]
dogs.find(dog => dog.name === 'Bernese Mountain Dog')
// {id: 'dog-2', name: 'Bernese Mountain Dog', ...etc}
dogs.some(dog => dog.temperament.includes('Aggressive'))
// false
dogs.some(dog => dog.temperament.includes('Trusting'))
// true
dogs.every(dog => dog.temperament.includes('Trusting'))
// false
dogs.every(dog => dog.temperament.includes('Intelligent'))
// true
dogs.map(dog => dog.name)
// ['Poodle', 'Bernese Mountain Dog', 'Labrador Retriever']
dogs.filter(dog => dog.temperament.includes('Faithful'))
// [{id: 'dog-1', ..etc}, {id: 'dog-2', ...etc}]
dogs.reduce((allTemperaments, dog) => {
  return [...allTemperaments, ...dog.temperaments]
}, [])
// [ 'Intelligent', 'Active', 'Alert', ...etc ]
// in React:
function RepositoryList({repositories, owner}) {
  return (
    <ul>
      {repositories
        .filter(repo => repo.owner === owner)
        .map(repo => (
          <li key={repo.id}>{repo.name}</li>
        ))}
    </ul>
  )
}
```

## [Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) and [async](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)/[await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/await)
```jsx
function promises() {
  const successfulPromise = timeout(100).then(result => `success: ${result}`)
  const failingPromise = timeout(200, true).then(null, error =>
    Promise.reject(`failure: ${error}`),
  )
  const recoveredPromise = timeout(300, true).then(null, error =>
    Promise.resolve(`failed and recovered: ${error}`),
  )
  successfulPromise.then(log, logError)
  failingPromise.then(log, logError)
  recoveredPromise.then(log, logError)
}
function asyncAwaits() {
  async function successfulAsyncAwait() {
    const result = await timeout(100)
    return `success: ${result}`
  }
  async function failedAsyncAwait() {
    const result = await timeout(200, true)
    return `failed: ${result}`
  }
  async function recoveredAsyncAwait() {
    let result
    try {
      result = await timeout(300, true)
      return `failed: ${result}` // this would not be executed
    } catch (error) {
      return `failed and recovered: ${error}`
    }
  }
  successfulAsyncAwait().then(log, logError)
  failedAsyncAwait().then(log, logError)
  recoveredAsyncAwait().then(log, logError)
}
function log(...args) {
  console.log(...args)
}
function logError(...args) {
  console.error(...args)
}
// This is the mothership of all things asynchronous
function timeout(duration = 0, shouldReject = false) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (shouldReject) {
        reject(`rejected after ${duration}ms`)
      } else {
        resolve(`resolved after ${duration}ms`)
      }
    }, duration)
  })
}
// in React:
function GetGreetingForSubject({subject}) {
  const [isLoading, setIsLoading] = React.useState(false)
  const [error, setError] = React.useState(null)
  const [greeting, setGreeting] = React.useState(null)
  React.useEffect(() => {
    async function fetchGreeting() {
      try {
        const response = await window.fetch('https://example.com/api/greeting')
        const data = await response.json()
        setGreeting(data.greeting)
      } catch (error) {
        setError(error)
      } finally {
        setIsLoading(false)
      }
    }
    setIsLoading(true)
    fetchGreeting()
  }, [])
  return isLoading ? (
    'loading...'
  ) : error ? (
    'ERROR!'
  ) : greeting ? (
    <div>
      {greeting} {subject}
    </div>
  ) : null
}
```

:memo: **참고 자료**   
* [https://kentcdodds.com/blog/javascript-to-know-for-react](https://kentcdodds.com/blog/javascript-to-know-for-react)   

