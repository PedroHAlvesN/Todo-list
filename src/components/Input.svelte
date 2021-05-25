<script>
    const todos = [
        {
            nome: "Fazer Compras",
            concluido: false
        },
        {
            nome: "Ir ao Dentista",
            concluido: true
        },
    ]
</script>

<style>
    .add-todo {
        padding: 10px 34px;
        font-family: "Open Sans";
        font-size: 20px;
        border: 0;
        outline: 0;
        max-width: 400px;
        width: 100%;
    }

    .add-todo::placeholder {
        color: rgba(0, 0, 0, 0.3);
        font-style: italic;
    }

    section {
        box-shadow: 0 2px 4px 0 rgb(0 0 0 / 20%), 0 25px 50px 0 rgb(0 0 0 / 10%);
        margin-bottom: 20px;
    }

    .todo {
        font-weight: 100;
        padding: 12px;
        display: flex;
        align-items: center;
        border: 1px solid #ededed;
    }

    .todo p {
        margin: 0 0 0 6px;
        color: #4d4d4d;
    }

    .todo input {
        display: flex;
        justify-content: center;
        align-items: center;
        appearance: none;
        height: 24px;
        width: 24px;
        border-radius: 50%;
        border: 1px solid rgba(175, 47, 47, 0.4);
    }

    .todo input:checked::after {
        content: '\2714';
        color: rgba(175, 47, 47, 0.4);
    }

    .todo input:checked ~ p {
        text-decoration: line-through;
        color: rgba(77, 77, 77, 0.5);
    }

</style>

<section>
    <input class="add-todo" type="text" placeholder="O que precisa ser feito?">
    {#each todos as todo}
        <div class="todo">
            <input type="checkbox">
            <p>{todo.nome}</p>
        </div>
    {/each}
</section>

