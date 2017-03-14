<template>
    <footer id="todo-footer">
        <div class="remain-cnt">
            {{remainItem}} left
        </div>
        <ul class="filters">
            <li v-for="filteri in filterArr">
                <a href="#" :class="{active : selected == filteri.toLowerCase() }">{{filteri}}</a>
            </li>
        </ul>
        <div class="clear-completed" @click="clearCompleted">
            Clear Completed
        </div>
    </footer>
</template>

<script>
export default {
    name: 'todo-footer',
    props: {
        remainings: Array
    },
    data: function(){
        return {
            filterArr: [
                'All',
                'Active',
                'Completed'
            ],
            selected : 'all'
        }
    },
    computed: {
        remainItem: function(){
            return this.remainings.length;
        }
    },
    methods: {
        clearCompleted: function (){
            this.$emit('clearCompleted');
        }
    }
}
</script>

<style lang="css">
    #todo-footer{display:flex; flex-flow:row nowrap; justify-content:space-around; align-items:center; position:relative; font-size:14px; color:#777;}
    #todo-footer:after{content:""; position:absolute; right:0; bottom:0; left:0; height:50px; overflow:hidden; box-shadow:0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6, 0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6, 0 17px 2px -6px rgba(0, 0, 0, 0.2);}
    #todo-footer .filters{position:relative; list-style:none; z-index:1;}
    #todo-footer .filters li{float:left;}
    #todo-footer .filters li a{color:inherit; text-decoration:none; margin:0 2px; padding:1px 4px; border:1px solid rgba(254,101,83,0); border-radius:3px;}
    #todo-footer .filters li a:hover{border:1px solid rgba(254,101,83,0.3);}
    #todo-footer .filters .active{border:1px solid rgba(254,101,83,1); border-radius:3px;}
    #todo-footer .filters .active:hover{border:1px solid rgba(254,101,83,1); border-radius:3px;}
    #todo-footer .clear-completed{position:relative; cursor:pointer; z-index:1;}
    #todo-footer .clear-completed:hover{text-decoration:underline;}
</style>
