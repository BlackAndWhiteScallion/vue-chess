<script>
import { reactive } from 'vue';
import { TheChessboard } from 'vue3-chessboard'; 
import 'vue3-chessboard/style.css'

export default{
  data: function(){
    return {
      history:''
    }
  },
  components:{
    TheChessboard
  },
  methods:{
    updateHistory(){
      this.history = this.boardAPI.getHistory();
    },
    showThreats(){
      var moves = this.boardAPI.getPossibleMoves();
      var threats = [];
      moves.forEach((value, key, map)=>{
        var piece = this.boardAPI.getSquare(key)
        if (piece){
          console.log(piece);
          if (piece.type == 'p'){
            if (key[0] != "a"){
              var left = this.pawnRange(key, true, piece.color);
              threats.push({orig:left, brush: 'yellow'});
              if (this.boardAPI.getSquare(left)){ 
                threats.push({orig:key, dest: left, brush: 'red'});
              }
            }
            if (key[0] != "h"){
              var right = this.pawnRange(key, false, piece.color);
              threats.push({orig: right, brush: 'yellow'});
              if (this.boardAPI.getSquare(right)){
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
      console.log(threats);
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
          <TheChessboard :board-config="boardConfig" @board-created="(api) => (boardAPI = api)" @move="updateHistory()"/>
        </div>
        <button @click="boardAPI.undoLastMove()">Undo</button>
        <button @click="boardAPI.toggleOrientation()">Flip Board</button>
        <button @click="boardAPI.toggleMoves()">Possible Moves</button>
        <button @click="showThreats()">Show Threats</button>
      </div>
      <div class="right-container">
        <p>{{ history }}</p>
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
  margin: 2rem;
}
.container{
  width: 100%;
}
.right-container{
  width: 40%;
}
.main-wrap{
  width: 500px;  
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
