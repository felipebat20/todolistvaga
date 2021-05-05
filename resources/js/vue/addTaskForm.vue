<template>
    <div class="addTask">
        <input type="text" v-model="task.name" @keyup.enter="addTask()"/>
        <font-awesome-icon
            icon="plus-square"
            @click="addTask()"
            :class="[task.name ? 'active': 'inactive', 'plus']"
            />
    </div>
</template>

<script>
export default {
    data: function(){
        return{
            task: {
                name:""
            }
        }
    },
    methods:{
        addTask(){
            if(this.task.name == ''){
                return;
            }

            axios.post('api/task/store', {
                task: this.task
            })
            .then( response => {
                console.log(response)
                if (response.status == 201 ){
                    this.task.name = "";
                    this.$emit('reloadList');
                } 
            })
            .catch( error => {
                console.log(error);
            })
        }
    }
}
</script>

<style scoped>
    .addTask{
        display: flex;
        justify-content: center;
        align-items: center; 
        cursor: pointer;
    }
    input{
        background: #f7f7f7;
        border: 0px;
        outline: none;
        padding: 5px;
        margin-right: 10px;
        width: 100%;
        height: 25px;
        font-size: 0.8em;
    }
     .plus{
          font-size: 20px;
     }
     .active{
        color: #00CE25; 
     }
     .inactive{
         color: #999999;
     }
</style>