<script lang="ts">
    type Todo = {
        text: string;
        done: boolean;
    };

    let newTodo = "";
    let todos: Todo[] = [];

    function addTodo() {
        if (!newTodo.trim()) return;
        todos = [...todos, { text: newTodo, done: false }];
        newTodo = "";
    }

    function toggleDone(i: number) {
        todos[i].done = !todos[i].done;
        todos = [...todos];
    }

    function removeTodo(i: number) {
        todos = todos.filter((_, idx) => idx !== i);
    }
</script>

<div class="wrapper">
    <h1>ToDo List</h1>

    <div class="input-row">
        <input
                placeholder="Add a task…"
                bind:value={newTodo}
                on:keydown={(e) => e.key === "Enter" && addTodo()}
        />
        <button class="add-btn" on:click={addTodo}>Add</button>
    </div>

    <ul class="todo-list">
        {#each todos as todo, i}
            <li class="todo">
                <label>
                    <input
                            type="checkbox"
                            checked={todo.done}
                            on:change={() => toggleDone(i)}
                    />
                    <span class:done={todo.done}>{todo.text}</span>
                </label>

                <button class="delete-btn" on:click={() => removeTodo(i)}>✕</button>
            </li>
        {/each}
    </ul>
</div>

<style>
    :global(body) {
        margin: 0;
        padding: 0;
        font-family: system-ui, sans-serif;
        background: #f4f4f7;
        display: flex;
        justify-content: center;
    }

    .wrapper {
        width: 100%;
        max-width: 600px;
        padding: 1.5rem;
        margin-top: 1.5rem;
        background: white;
        border-radius: 16px;
        box-shadow: 0 6px 20px rgba(0, 0, 0, 0.08);
    }

    h1 {
        text-align: center;
        margin-bottom: 1.3rem;
        font-weight: 700;
    }

    /* Input row */
    .input-row {
        display: flex;
        gap: 0.5rem;
    }

    input {
        flex: 1;
        padding: 0.8rem 1rem;
        font-size: 1rem;
        border: 2px solid #ddd;
        border-radius: 12px;
        outline: none;
        transition: border 0.2s;
    }

    input:focus {
        border-color: #31bd8c; /* cute purple highlight */
    }

    .add-btn {
        padding: 0.8rem 1.4rem;
        background: #31BD8CFF;
        color: white;
        border: none;
        border-radius: 12px;
        font-size: 1rem;
        cursor: pointer;
        transition: background 0.2s, transform 0.1s;
    }

    .add-btn:hover {
        background: #31BD8CFF;
    }

    .add-btn:active {
        transform: scale(0.97);
    }

    /* Todo items */
    .todo-list {
        list-style: none;
        padding: 0;
        margin: 1.3rem 0 0;
        display: flex;
        flex-direction: column;
        gap: 0.6rem;
    }

    .todo {
        background: #fafafa;
        padding: 0.9rem 1rem;
        border-radius: 12px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 1rem;
        border: 1px solid #eaeaea;
    }

    label {
        display: flex;
        align-items: center;
        gap: 0.6rem;
        flex: 1;
    }

    .done {
        text-decoration: line-through;
        opacity: 0.6;
    }

    .delete-btn {
        background: none;
        border: none;
        font-size: 1.1rem;
        cursor: pointer;
        color: #ff5e6c;
        padding: 0.3rem 0.6rem;
        border-radius: 8px;
        transition: background 0.2s;
    }

    .delete-btn:hover {
        background: rgba(255, 94, 108, 0.1);
    }

    @media (max-width: 500px) {
        .input-row {
            flex-direction: column;
        }

        .add-btn {
            width: 100%;
        }
    }
</style>
