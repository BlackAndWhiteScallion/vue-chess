<template>

</template>

<style>
.collapse-enter-active,
.collapse-leave-active {
    transition: all 0.2s;
}
.collapse-enter,
.collapse-leave-to {
    opacity: 0;
    transform: translateX(-100%);
}
</style>

<script>
export default{
    data(){
        return{
            isCollapse:false
        }
    },
    methods:{
        toggleCollapse(){
            this.isCollapse = !this.isCollapse;
        }
    }
}
</script>
