<script lang="ts">
    type Todo = {
        text: string;
        done: boolean;
    };

    let newTodo = "";
    let todos: Todo[] = [];
    let totalCount = 0;
    let doneCount = 0;

    function addTodo() {
        if (!newTodo.trim()) return;
        todos = [...todos, { text: newTodo, done: false }];
        newTodo = "";
        totalCount++;
    }

    function toggleDone(i: number) {
        if (todos[i].done) {
            doneCount--;
            totalCount++;
        } else {
            doneCount++;
            totalCount--;
        }
        todos[i].done = !todos[i].done;
        todos = [...todos];
    }

    function removeTodo(i: number) {
        if (todos[i].done) doneCount--;
        else totalCount--;
        todos = todos.filter((_, idx) => idx !== i);
    }
</script>

<div class="wrapper">
    <h1>Your To Do</h1>

    <div class="input-row">
        <input
                placeholder="Add new task"
                bind:value={newTodo}
                on:keydown={(e) => e.key === "Enter" && addTodo()}
        />
        <button class="rounded-btn" on:click={addTodo}><i class="fa-solid fa-plus"></i></button>
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

    <p class="remaining">
        Your remaining todos : {totalCount}
    </p>

    <p class="quote">
        "Doing what you love is the cornerstone of having abundance in your life."
        <br />– Wayne Dyer
    </p>
</div>

<style>
    :global(body) {
        margin: 0;
        padding: 0;
        min-height: 100vh;
        font-family: system-ui, sans-serif;
        display: flex;
        justify-content: center;
        align-items: flex-start;
    }

    .wrapper {
        width: 100%;
        max-width: 700px;
        padding: 2rem 1.5rem;
        margin-top: 3rem;
        background: white;
        border-radius: 20px;
    }

    h1 {
        margin-bottom: 1rem;
        font-weight: 700;
        font-size: 1.8rem;
    }

    .input-row {
        display: flex;
        align-items: center;
        gap: 0.7rem;
        margin-bottom: 1.2rem;
    }

    input {
        flex: 1;
        padding: 0.8rem 0rem;
        font-size: 1rem;
        border: none;
        border-bottom: 2px solid #ddd;
        outline: none;
        transition: 0.2s;
    }

    input:focus {
        border-color: #666;
    }

    .rounded-btn {
        width: 36px;
        height: 36px;
        border-radius: 12px;
        border: none;
        background: #444;
        color: white;
        font-size: 1rem;
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
        transition: 0.2s;
    }


    .rounded-btn:hover {
        background: #333;
    }

    .todo-list {
        list-style: none;
        padding: 0;
        display: flex;
        flex-direction: column;
        gap: 0.8rem;
    }

    .todo {
        background: white;
        border: 1px solid #ddd;
        padding: 0.9rem 1rem;
        border-radius: 14px;
        display: flex;
        align-items: center;
        justify-content: space-between;
        gap: 1rem;
    }

    label {
        display: flex;
        align-items: center;
        gap: 0.6rem;
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
        color: #c44;
        padding: 0.3rem 0.6rem;
        border-radius: 8px;
        transition: background 0.2s;
    }

    .delete-btn:hover {
        background: rgba(255, 94, 108, 0.1);
    }

    .remaining {
        margin-top: 1rem;
        font-weight: 600;
        color: #555;
    }

    .quote {
        margin-top: 0.5rem;
        font-style: italic;
        font-size: 0.9rem;
        color: #888;
    }

    /* Responsive */
    @media (max-width: 600px) {
        .wrapper {
            margin-top: 1rem;
            padding: 1.2rem;
        }

        .input-row {
            gap: 0.5rem;
        }

        .rounded-btn {
            width: 36px;
            height: 36px;
        }
    }
</style>
