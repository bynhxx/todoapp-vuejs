<template>
    <div id="task">
        <form @submit.prevent="addTask">
            <input 
            v-model="tarefa"
            type="text"
            placeholder="Insira uma tarefa"
            />
            <button type="submit">Adcionar</button>
        </form>
        <Item :lista="tarefas" :delete="deleteTask"/>

        <span v-show="tarefas.length">
            Você tem <strong :class="{pend: pendente}"> {{tarefas.length}} </strong> tarefas pendentes
        </span>

    </div>
</template>

<script>
import Item from './Item'
export default {
    name: 'Task',
    components: {
        Item
    },
    data(){
        return{
            tarefa: '', 
            tarefas: [],
            pendente: true
        }
    },
    methods: {
        addTask(){ 
            if(this.tarefa !== ''){
                this.tarefas.push({
                    text: this.tarefa,
                    key: Date.now()
                })
                this.tarefa = ''
            } else {
                alert('Digite uma tarefa')
                return
            }
            console.log(this.tarefas)
        },
        deleteTask(key){
            let filtro = this.tarefas.filter((item) => {
                return item.key !== key
            })
            return this.tarefas = filtro
        }
    }, 
    watch:{
        tarefas:{
            deep: true, 
            handler(){
                localStorage.setItem('tasks', JSON.stringify(this.tarefas))
                this.tarefas.length > 4 ? this.pendente = true : this.pendente = false
            }
        }
    },
    created(){
        const mylist = localStorage.getItem('tasks')
        this.tarefas = JSON.parse(mylist) || []
    }

}
</script>

<style scoped>
    #task{
        max-width: 700px;
        background-color: #e6e6e6;
        border-radius: 5px;
        padding: 20px; 
        margin: 20px auto;
        box-shadow: 0 0 20px #00000065;
    }
    form{
        margin-top: 30px;
        display: flex;
        flex-direction: row;
    }

    form button{
        cursor: pointer;
        background-color: #2b476a ;
        color: white;
        outline: none;
        border: none; 
        border-radius: 5px;
        padding: 7px 15px; 
        margin-left: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    input{
        flex: 1; 
        border: 1px solid #8794aa96; 
        padding: 7px; 
        outline: none;
    }

    span{
        color: #2b476a; 
    }

    .pend{
        color: red; 
    }
</style>