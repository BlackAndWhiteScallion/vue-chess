<template>
    <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="Move" label="Move" />
    </el-table>
</template>

<style scoped>

</style>

<script>

export default{
    computed:{
        tableData:function(){
            return [
                {
                    
                }
            ];
        }
    },
    props:{
    },
    methods:{

    },
}
</script>