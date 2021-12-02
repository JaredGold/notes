# useContext
Context is used to share a value to all of the children components without needing prop drilling. We create  the context with `React.createContext()` or `createContext()`. We then wrap the children components with a `<ContextName.Provider value={passedValue} >` 
This will look like below:
```js
import { createContext, useState } from 'react'

export const ThemeContext = createContext()

const App = () => {
	const [darkTheme, setDarkTheme] = useState(true)
	
	function toggleTheme() => {
		setDarkTheme(prevDarkTheme => !prevDarkTheme)
	}
	
	return (
		<>
			<ThemeContext.Provider value={darkTheme}>
				<button onClick={toggleTheme}>Toggle Teheme</button>
				<ChildComponent />
			</ThemeContext.Provider>
		</>
	)
}

```

We use the hook useContext to pull the assign the context to a child value
```js
import { ThemeContext } from './App'

export default function ChildComponent() {
	const darkTheme = useContext(ThemeContext) // Context we imported from parent
	return <div>Theme</div>
}

```
