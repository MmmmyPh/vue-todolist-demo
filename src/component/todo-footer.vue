<template>
    <footer id="todo-footer">
        <div class="remain-cnt">
            {{remainItem}} left
        </div>
    </footer>
</template>

<script>
export default {
    name: 'todo-footer',
    props: {
        remainings: Array
    },
    computed: {
        remainItem: function(){
            return this.remainings.length;
        }
    },
    methods: {

    }
}
</script>

<style lang="css">
</style>
