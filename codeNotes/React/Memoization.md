# Memoization
Memoization in short is the premise of saving data inside of the cache as apposed to redoing a function which has already been done. Sometimes this may not matter but in longer more complex functions it can be the difference between a slow function and a fast function.

The below is a function which calculates the value of a number plus 2. This will save that value into an object called cache. If the function has been run with that value it does not do the calculation and simply pulls the data from the cache.

```js
const cache = {}

function addTwo(input) {

 if (!cache.hasOwnProperty(input)) {

 cache[input] = input + 2

 }

 return cache[input]

}
```

## Memoization in React
React has  three APIs for memoization `memo`, `useMemo` and `useCallback`. React currently only stores cache of the most recent value of an input and it's result. Similar to the above function the below function is more similar but written in the same way it would be written in React.

```js
let prevInput, prevResult

function addTwo(input) {
	if (input !== prevInput) {
		prevResult = input + 2
	}
	prevInput = input
	return prevResult
}
```