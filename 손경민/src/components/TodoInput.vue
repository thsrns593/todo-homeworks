<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
            <i class="fas fa-plus addBtn"></i>
        </span>
        <modal v-if="showModal" @close="showModal = false">
            <h3 slot="header">error!
                <i class="fas fa-times closeModal" @click="showModal = false"></i>
            </h3>
            <h5 slot="body">할 일을 입력하세요.</h5>
        </modal>
    </div>
</template>

<script>
import modal from './common/modal.vue';

export default {
    data: function(){
        return{
            newTodoItem: "",
            showModal: false
        }
    },
    methods: {
        addTodo: function(){
            if(this.newTodoItem !== ""){
                this.$emit("add", this.newTodoItem);
                this.clearInput();
            }else{
                this.showModal = !this.showModal;
            }
        },
        clearInput: function(){
            this.newTodoItem = "";
        }
    },
    components: {
        'modal': modal
    }
}
</script>

<style scoped>
input:focus {
    outline: none;
}
.inputBox{
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input{
    border-style: none;
    font-size: 0.9rem;
}
.addContainer{
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn{
    color: white;
    vertical-align: middle;
}
.closeModal{
    color: red;
}
</style>
