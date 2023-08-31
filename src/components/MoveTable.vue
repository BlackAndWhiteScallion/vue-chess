<template>
    <el-table :data="tableData" border style="width: 100%" @cell-click="rewind">
        <el-table-column prop="Move" label="Move" width="80"/>
        <el-table-column prop="White" label="White"  />
        <el-table-column prop="Black" label="Black" />
    </el-table>
</template>

<style scoped>
    
</style>

<script>
export default{
    computed:{
        tableData:function(){
            if (!this.moveset) return [];
            var moves = []; 
            for (var i = 1; i <= this.moveset.length; i += 2){
                moves.push({
                    Move: Math.round(i/2),
                    White: this.moveset[i-1] || null,
                    Black: this.moveset[i] || null,
                })
            }
            return moves;
        }
    },
    props:['moveset'],
    emits:['rewindHistory'],
    setup(props){
        console.log(props);
    },
    methods:{
        rewind:function(row, column, cell){
            this.$emit('rewindHistory', row.Move * 2 - (column.property == "White" ? 1 : 0));
        }
    },
}
</script>