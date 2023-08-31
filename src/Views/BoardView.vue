<script>
import { reactive } from 'vue';
import { ref } from 'vue'
import { TheChessboard } from 'vue3-chessboard'; 
import 'vue3-chessboard/style.css'
import MoveTable from '../components/MoveTable.vue';
import PossibleTable from '../components/PossibleTable.vue'

export default{
  data: function(){
    return {
	    activeName: ref('first'),
      history:[''],
	    moves:'',
    }
  },
  components:{
    TheChessboard,
    MoveTable,
    PossibleTable
  },
  methods:{
    updateHistory(){
      this.history = this.boardAPI.getHistory();
    },
    updateMoves(){
      this.moves = this.boardAPI.getPossibleMoves();
    },
    showThreats(){
      var moves = this.boardAPI.getPossibleMoves();
      var threats = [];
      moves.forEach((value, key, map)=>{
        var piece = this.boardAPI.getSquare(key)
        if (piece){
          if (piece.type == 'p'){
            if (key[0] != "a"){
              var left = this.pawnRange(key, true, piece.color);
              threats.push({orig:left, brush: 'yellow'});
              var leftpiece = this.boardAPI.getSquare(left);
              if (leftpiece && leftpiece.color != piece.color){ 
                threats.push({orig:key, dest: left, brush: 'red'});
              }
            }
            if (key[0] != "h"){
              var right = this.pawnRange(key, false, piece.color);
              threats.push({orig: right, brush: 'yellow'});
              var rightpiece = this.boardAPI.getSquare(right);
              if (rightpiece && rightpiece.color != piece.color){
                threats.push({orig:key, dest: right, brush: 'red'});
              }
            }
          } else {
            value.forEach((element) => {
              threats.push({orig: element, brush: 'yellow' });
              if (this.boardAPI.getSquare(element)){
                threats.push({orig:key, dest: element, brush: 'red'});
              }
            });
          }
        }
      });
      this.boardAPI.setShapes(threats);
    },
    pawnRange(key, left, color){
        return String.fromCharCode(key.charCodeAt(0)+ (left ? -1 : 1)) + (parseInt(key[1]) + (color == "w" ? 1 : -1));
    },
  },
  created(){
     this.boardConfig = reactive({
      coordinates: true,
      autoCastle: false,
      orientation: 'white',
    });
    this.boardAPI;
  }
}

</script>

<template>
  <main>
    <body>
      <div class="left-container">
        <div class="board-container">
          <TheChessboard :board-config="boardConfig" @board-created="(api) => (boardAPI = api)" @move="updateHistory();updateMoves()"/>
        </div>
		<div class="button-container">
			<button @click="boardAPI.undoLastMove();updateHistory();updateMoves()">Undo</button>
			<button @click="boardAPI.toggleOrientation()">Flip Board</button>
			<button @click="showThreats()">Show Threats</button>
		</div>
      </div>
      <div class="right-container">
		<el-tabs v-model="activeName" class="demo-tabs">
    		<el-tab-pane label="History" name="first">
				<MoveTable :moveset="history"  @rewindHistory="(n) => boardAPI.viewHistory(n)"/>
			</el-tab-pane>
    		<el-tab-pane label="Possible Moves" name="second">
          <PossibleTable :moveset="moves"/>
			</el-tab-pane>
  		</el-tabs>
      </div>
    </body>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}
body{
  display: flex;
  align-content: space-evenly;
  justify-content: space-evenly;
  margin: 2rem;
}
.container{
  width: 100%;
}
.button-container{
	display: flex;
	margin-top: 0.5rem;
	justify-content: space-between;
}
.right-container{
  width: 40%;
}
.main-wrap{
  width: 500px;  
}
.demo-tabs > .el-tabs__content {
  padding: 32px;
  color: #6b778c;
  font-size: 32px;
  font-weight: 600;
}

@media (min-width: 1024px) {

}
</style>
