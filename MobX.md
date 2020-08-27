# About TypeScript
### Keturah Howard, June 8th 2020
referencing 
- [this youtube tutorial (refered to throughout page as `father vid`)](https://www.youtube.com/watch?v=_q50BXqkAfI)
- [these mobx docs (reffered to as `father doc`)](https://mobx.js.org/README.html)
## *Description*

A state management library : simple, scalable via TFRP (transparently applying reactive programming)
Used in place of Redux/other state management tools

*Diagram of how it works*
<img width="801" alt="Screen Shot 2020-06-08 at 3 33 30 PM" src="https://user-images.githubusercontent.com/32975967/84086742-6eaccf00-a99d-11ea-9cde-e0de0587ef76.png">

*Describing Diagram*
1. Events evoke *actions*, actions are the only thing that modify state
2. state is **observable**, minimally defined
3. computed values are derividiv of state using a pure function.. updated automatically using MobX 
4. reactions are like computed values and react to state changes, but produce side effects instead of values, and this restarts the process

## Core Concepts

### Observable state
- adds observable capabilities to exixsting data structures (objects, arrays, class instances)
- done by adding @observable infront of class properties with ```@observable``` devorator
``` 
import { observable } from "mobx"

class Todo {
    id = Math.random()
    @observable title = ""
    @observable finished = false
}
```
### Computed values
values that have been defined to derive automatically from relevent data. 
- done with ```@computed``` decorator
```
class TodoList {
    @observable todos = []
    @computed get unfinishedTodoCount() {
        return this.todos.filter(todo => !todo.finished).length
    }
}
```
unfinishedTodoCount is a number prop of TodoList that will automatically update when todos are created/their finished props are modified

### Reactions

these too are manipulated by relavent data, only instead of rendering values they make changes within the app (print to console, make network reqs, incrementally updating the React component tree to patch the DOM)

father doc: "In short, reactions bridge reactive and imperative programming."

#### ways to implement

1. In react, you can make an entire (stateless function) component reactive by adding @observer decorator above:

```
import { observer } from "mobx-react"

@observer
class TodoListView extends Component {
  render() {
    ...
    <ul>
      {this.props.todoList.todos.map(todo => (
        <TodoView todo={todo} key={todo.id} />
      ))}
    </ul>
    ...
  }

  const TodoView = observer(({ todo }) => (
    <li>
      <input
        type="checkbox"
        checked={todo.finished}
        onClick={() => (todo.finished = !todo.finished)}
      />
      {todo.title}
    </li>
  ))
```
**need to come back to this when I better understand it**

***Following along with tutorial used to create [Goalsplain](https://github.com/KeturahDev/goalsplain)***

Cool notes:
- create a store folder to have your mobx store files for different pieces of applications storage: up to you how you want to divide info up!