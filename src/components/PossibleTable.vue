<template>
    <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="Piece" label="Piece" />
        <el-table-column prop="Square" label="Square" />
        <el-table-column prop="Move" label="Move" />
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
            for (const [key, value] of this.moveset) {
                for (var i = 0; i < value.length; i ++){
                    console.log(value[i]);
                    moves.push({
                        Piece: null,
                        Square: key,
                        Move: value[i],
                    })
                }
            }
            return moves;
        }
    },
    props:['moveset'],
    emits:['displaymove'],
    setup(props){
        console.log(props);
    },
    methods:{

    },
}
</script>