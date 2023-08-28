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
      this.history = this.boardAPI.getPossibleMoves();
    },
    showThreats(){
      let moves = this.boardAPI.getPossibleMoves();
      for (var i in moves){
        if (true){

        }
      }
    }
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
        <button @click="boardAPI.toggleMoves()">Show Threats</button>
      </div>
      <div>
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
}
.container{
  width: 100%;
}

.main-wrap{
  width: 400px;  
}

.logo {
  display: block;
  margin: 0 auto 2rem;
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
