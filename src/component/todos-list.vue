<template>
    <section id="todos-list">
        <input type = "checkbox"
                class = "toggle-all"
                v-model = "toggleAll">
        <ul class="list">
            <li v-for="(todo, index) in todoLists"
                :class="{isChosen : todo.todoDone}">
                <input type="checkbox"
                        class = "toggle-single"
                        @click="toggleCompleteThis(index)">
                <label for="">{{todo.todoTitle}}</label>
                <button class="destroy"
                        @click="deleteThis(index)"></button>
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    name: 'todos-list',
    props: {
        todoLists: Array,
        remains: Array
    },
    data: function() {
        return {

        }
    },
    computed: {
        toggleAll: {
            get: function(){
                return this.remains.length === 0;
            },
            set: function(value){
                this.toggleAllEve(value);
            }
        }
    },
    methods: {
        toggleCompleteThis: function(index){
            this.$emit('toggleCompleteThis', index);
        },
        deleteThis: function(index){
            this.$emit('deleteThis', index);
        },
        toggleAllEve: function(val){
            this.$emit('toggleAllEve', val);
        }
    }
}
</script>

<style lang="css">
    #todos-list{position:relative;}
    #todos-list .toggle-all{position:absolute; left:-5px; top:-50px; width:60px; height:30px; text-align:center; background:none; border:none; transform:rotate(90deg); -webkit-appearance:none; appearance:none; outline:none;}
    #todos-list .toggle-all:after{content:"❯"; padding:10px 27px; font-size:22px; color:rgb(230,230,230);}
    #todos-list .toggle-all:checked:after{color:#737373;}

    #todos-list .list{margin:0; padding:0; list-style:none;}
    #todos-list .list li{position:relative; border-bottom:1px solid #ededed;}
    #todos-list .list li:last-child{border-bottom:none;}
    #todos-list .list .toggle-single{position:absolute; left:9px; top:0; bottom:0; margin:auto; width:40px; height:40px; background:none; border:none; -webkit-appearance:none; appearance:none; outline:none;}
    #todos-list .list .toggle-single:after{content:""; display:block; width:40px; height:40px; border:1px solid #ececec; border-radius:50%;}
    #todos-list .list label{display:block; margin-left:45px; padding:15px 60px 15px 15px; font-size:24px; text-align:left; line-height:1.2; transition:color 0.4; word-break:break-all; transition:color 0.2s ease-out;}
    #todos-list .list .destroy{position:absolute; right:10px; top:0; bottom:0; margin:auto; height:40px; width:40px; font-size:30px; color:#cc9a9a; transition:color 0.2s ease-out; background:none; border:none; -webkit-appearance:none; appearance:none; outline:none;}
    #todos-list .list .destroy:after{content:"×"}
    #todos-list .list .destroy:hover{color:#af5b5e;}
    #todos-list .list .isChosen .toggle-single:after{background:url("../assets/chosen.svg") no-repeat center center;border-color:rgba(52,188,152,0.3);}
    #todos-list .list .isChosen label{color:#999; text-decoration:line-through;}
</style>
