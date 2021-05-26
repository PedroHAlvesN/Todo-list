<script>
import { loop_guard } from "svelte/internal"

    const numeroAleatorio = (min, max) => Math.round(Math.random() * (max - min) + min)
    
    let todos = [
        {
            id: numeroAleatorio(1, 100000),
            nome: "Fazer Compras",
            concluido: false,
            editando: false
        },
        {
            id: numeroAleatorio(1, 100000),
            nome: "Ir ao Dentista",
            concluido: true,
            editando: false
        }
    ]

    const adicionarTodo = evento => { 
        const nomeTodo = evento.target.value
        if (evento.charCode === 13) {
            todos = [...todos, {
                id: numeroAleatorio(1, 100000),
                nome: nomeTodo, 
                concluido: false, 
                editando: false 
            }]
            evento.target.value = ""
        }
    }

    const obterTodoPorId = id => todos.findIndex(todo => id === todo.id)

    const editarTodo = (id, todoPropriedade, todoValor) => {
        const todoIndice = obterTodoPorId(id)
        todos[todoIndice][todoPropriedade] = todoValor
        todos = todos
    }

    const alterarStatusEdicao = id => {
        const todoIndice = obterTodoPorId(id)
        const editandoInvertido = !todos[todoIndice].editando
        editarTodo(id, "editando", editandoInvertido)
    }

    const editarNomeTodo = (evento, id) => {
        if (evento.charCode === 13) {
            const novoNomeTodo = evento.target.value
            editarTodo(id, "nome", novoNomeTodo)
            alterarStatusEdicao(id)
        }
    }

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

    .todo input[type="checkbox"] {
        display: flex;
        justify-content: center;
        align-items: center;
        appearance: none;
        height: 24px;
        width: 24px;
        border-radius: 50%;
        border: 1px solid rgba(175, 47, 47, 0.4);
    }

    .todo input[type="checkbox"]:checked::after {
        content: '\2714';
        color: rgba(175, 47, 47, 0.4);
    }

    .todo input[type="checkbox"]:checked ~ p {
        text-decoration: line-through;
        color: rgba(77, 77, 77, 0.5);
    }
</style>

<section>
    <input on:keypress={adicionarTodo} class="add-todo" type="text" placeholder="O que precisa ser feito?">
    {#each todos as todo}
        <div class="todo">
            <input type="checkbox">
            {#if todo.editando}
                <input on:keypress={evento => editarNomeTodo(evento, todo.id)} type="text">
            {:else}
                <p on:dblclick={() => alterarStatusEdicao(todo.id)}>{todo.nome}</p>
            {/if}
        </div>
    {/each}
</section>

