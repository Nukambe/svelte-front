<script>
  import { v4 as uuid } from "uuid";
  import TodoList from "./lib/TodoList.svelte";

  let todoList;

  let todos = [
    { id: uuid(), title: "todo 1", completed: true },
    { id: uuid(), title: "todo 1", completed: false },
    { id: uuid(), title: "todo 1", completed: true },
  ];

  $: console.log(todos);

  function handleAddTodo(event) {
    event.preventDefault();
    setTimeout(() => {
      todos = [
        ...todos,
        { id: uuid(), title: event.detail.title, completed: false },
      ];
      todoList.clearInput();
    }, 0);
  }

  function handleRemoveTodo(event) {
    todos = todos.filter((todo) => todo.id !== event.detail.id);
  }

  function handleToggleTodo(event) {
    todos = todos.map((todo) => {
      if (todo.id !== event.detail.id) return todo;
      return { ...todo, completed: event.detail.value };
    });
  }
</script>

<p>{todoList?.readonly}</p>
<h2>{todos.length} Todos</h2>
<TodoList
  {todos}
  bind:this={todoList}
  on:addtodo={handleAddTodo}
  on:removetodo={handleRemoveTodo}
  on:toggletodo={handleToggleTodo}
/>

<button on:click={() => todoList.focusInput()}>Focus Input</button>

<style>
</style>
