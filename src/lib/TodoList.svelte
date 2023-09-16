<svelte:options immutable={true} />

<script>
    import { createEventDispatcher, onMount, onDestroy } from "svelte";
    import { v4 as uuid } from "uuid";
    import Button from "./Button.svelte";

    export let todos = [];
    export const readonly = 'read only';
    export function clearInput() {
        inputText = '';
    }
    export function focusInput () {
        input.focus();
    }
    onMount(() => {
        console.log('mounted')
    })
    onDestroy(() => {
        console.log('destroyed')
    })
    let inputText = "";
    let input, divListHeight;
    const dispatch = createEventDispatcher();

    function handleAddTodo() {
        //     if (!inputText) return;
        //     // todos.push({ id: uuid(), title: inputText, completed: false});
        //     // todos = todos;
        //     todos = [...todos, { id: uuid(), title: inputText, completed: false}];
        //     inputText = '';
        const isNotCancelled = dispatch(
            "addtodo",
            {
                title: inputText,
            },
            { cancelable: true }
        );
        if (isNotCancelled) {
            inputText = "";
        }
    }

    function handleRemoveTodo(id) {
        dispatch("removetodo", { id });
    }

    function handleToggleTodo(id, value) {
        dispatch("toggletodo", { id, value });
    }
</script>

{divListHeight}
<div class="todo-list-wrapper" bind:offsetHeight={divListHeight}>
    <ul>
        {#each todos as todo (todo.id)}
            <!-- {@const number = index + 1} -->
            <li>
                <label for={todo.id}>{todo.title}</label>
                <input
                    type="checkbox"
                    name={todo.id}
                    on:input={(event) => {
                        event.currentTarget.checked = todo.completed;
                        handleToggleTodo(todo.id, !todo.completed)
                    }}
                    checked={todo.completed}
                />
                <button on:click={() => handleRemoveTodo(todo.id)}
                    >Remove</button
                >
            </li>
        {/each}
    </ul>
    <form class="add-todo-form" on:submit|preventDefault={handleAddTodo}>
        <input bind:this={input} bind:value={inputText} />
        <Button type="submit" size="large" disabled={!inputText}>Add</Button>
    </form>
</div>
