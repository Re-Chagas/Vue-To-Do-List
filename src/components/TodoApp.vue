<template>
    <div class="contianer">
        <h2 class="text-center mt-5">My Vue Todo App</h2>

        <!--Input-->
        <div class="d-flex">
            <input v-model="task" type="text" placeholder="Enter Task" class="form-control">
            <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
        </div>

        <!--task table-->
        <table class="table table-bordered mt-5">
            <thead>
                <tr>
                    <th scope="col">Task</th>
                    <th scope="col">Status</th>
                    <th scope="col" class="text-center">#</th>
                    <th scope="col" class="text-center">#</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(task, index) in tasks" :key="index">
                    <td>
                        <span :class="{'finished': task.status === 'finished'}">{{ task.name }}</span>
                    </td>
                    <td>
                        <span @click="changeStatus(index)" class="pointer" 
                        :class="{'tex-danger': task.status === 'to-do',
                        'text-warning': task.status ==='to-do',
                        'text-success': task.status ==='finished'}"
                        >
                            {{firstCharUpper(task.status) }} 
                        </span>
                    </td>
                    <td>
                        <div class="text-center" @click="editTask(index)">
                            <span class="fa fa-pen"></span>
                        </div>
                    </td>
                    <td>
                        <div class="text-center" @click="deleteTask(index)">
                            <span class="fa fa-trash"></span>
                        </div>
                    </td>
                    <td></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'HelloWorld',
    props: {
        msg: String,
    },
    data() {
        return {
            task:'',
            editedTask: null,
            availableStatuses:['to-do', 'in-progress', 'finished' ],

            tasks: [
                {
                    name: '',
                    status: '',
                },
                {
                    name: '',
                    status: '',
                }
            ],
        };
    },

    methods: {
        submitTask(){
            if (this.task.length === 0) return;

            if (this.editedTask === null) {
                this.task.push({
                name: this.task,
                status: 'to-do'
            })   
            }else{
                 this.tasks[this.editedTask].name = this.task;
                 this.editTask = null;
            }

            this.task = '';
        },

        deleteTask(index){
            this.task.splice(index, 1)
        },

        editTask(index){
            this.tasks = this.taks[index].name;
            this.editedTask = index;
        },

        changeStatus(index){
         let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
         if (++newIndex > 2) newIndex = 0
         this.tasks[index].status = this.availableStatuses[newIndex];
        },

        firstCharUpper(str){
            return str.charAt(0).toUpperCase() + str.slice(1);
        }
    }
};
</script>


<style scoped>
.pointer{
    cursor: pointer;
}

.finished{
    text-decoration: line-through;
}

</style>