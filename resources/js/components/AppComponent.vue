<template>
    <div id="app">

        
        <div class="col-md-12">
           <form-component @new="addTask"></form-component>
        </div>
        
        <div class="col-md-12">
            <div class="card mb-4 shadow-sm">
                <div class="card-header">Lista De Tarefas</div>
                <div class="card-body">
            
                <task-component 
                    v-for="(task, index) in tasks" 
                    :key="task.id" 
                    :task="task" 
                    @update="updateTask(index, task)"
                    >
                </task-component>
                </div>
            </div>
        </div> 
        
        <modal-component v-if="modalOpen" :modalOpen="modalOpen" ></modal-component>

    </div>
    
</template>

<script>
    export default {
        data() {
            return {
                tasks: [],
                modalOpen: false
            }
        },
        mounted() {
            axios.get('/tasks').then((response) => {
                
                this.tasks = response.data;

            })
        },
        methods: {
            addTask(task){   
                this.tasks.push(task);
            },
            updateTask(index, task){
                this.openModal()
                this.tasks[index] = task;
            },
            openModal() {
                this.modalOpen = !this.modalOpen;

            }
        }
    }
</script>