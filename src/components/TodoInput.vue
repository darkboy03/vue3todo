<template>
    <div class="inputBox shadow">
        <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
        <span class="addContainer" @click="addTodo">
            <i class="material-symbols-outlined addBtn">add</i>
        </span>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                newTodoItem : "",
                showModal : false
            }
        },
        methods: {
            addTodo() {
                if(this.newTodoItem !== ''){
                    console.log(this.newTodoItem);
                    this.$emit('addTodoItem', this.newTodoItem);
                    this.clearInput(); 
                }else {
                    this.showModal = !this.showModal;
                }
            },
            clearInput() {
                this.newTodoItem = '';
            }

        }
    }
</script>

<style>
input:focus {
    outline: none;
}

.inputBox {
 background: white;
 height: 50px;
 line-height: 50px;
 border-radius: 5px;
}

.inputBox input {
 border-style: none;
 font-size: 0.9rem;
}

.addContainer {
 float : right;
 background: linear-gradient(to right, #6378FB, #8763FB);
 display: block;
 width: 3rem;
 border-radius: 0 5px 5px 0; 
}

.addBtn {
    color : white;
    vertical-align: middle;
}
</style>