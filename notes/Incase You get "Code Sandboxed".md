```import "./styles.css";

import { useState, createContext } from "react";

import ListOfTodo from "./components/ListOfTodo/ListOfTodo";

import TodoForm from "./components/TodoForm/TodoForm";

import { Todos, Todo } from "./types";

  

const createNewId = (todos: Todos) => {

if (todos.length === 0) return 1;

return todos[todos.length - 1].id + 1;

};

  

type TodosData = {

todos: Todos;

addTodo: (todoTitle: string) => void;

updateTodo: (id: number, overrides: Partial<Todo>) => void;

};

  

export const TodosContext = createContext<undefined | TodosData>(undefined);

  

type Props = {

children: React.ReactNode;

};

  

export const TodosProvider = (props: Props) => {

const [todos, updateTodos] = useState<Todos>([]);

  

const addTodo = (todoTitle: string) => {

let newTodo = {

// look into converting id to UUID using package

id: createNewId(todos),

title: todoTitle,

complete: false,

removed: false

};

  

updateTodos([...todos, newTodo]);

};

  

const updateTodo = (id: number, overrides: Partial<Todo>) => {

const updatedTodos = todos.map((todo) => {

if (todo.id === id) {

return {

...todo,

...overrides

};

}

return todo;

});

updateTodos(updatedTodos);

};

  

const value = { todos, addTodo, updateTodo };

  

return <TodosContext.Provider value={value} {...props} />;

};

  

const App = () => {

return (

<div>

<h1>TODO's</h1>

<TodosProvider>

<TodoForm />

<ListOfTodo />

</TodosProvider>

</div>

);

};

  

export default App;
```