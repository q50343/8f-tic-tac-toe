<template>
  <div class="backgroundRed">
    <div class="container">
      <div class="header">
        <div class="inline-block bgB" :class='{redB:player===-1}'>
          <div class="x"></div>
        </div>
        <div class="inline-block num">{{winX}}</div>
        <div class="inline-block vs bgB">vs</div>
        <div class="inline-block num">{{winO}}</div>
        <div class="inline-block bgB" :class='{redB:player===1}'>
          <div class="o"></div>
        </div>
      </div>
			<p class="turn" :class='{right:player=== 1}'>YOUR TURN!</p>
			<div class="board" v-if='!winner && !draw'>
				<div 
					class="grids" 
					v-for='(grid,id) in grids' :key="id"
					@click='set(id)'>
					<div :class='get(grid)'></div>
				</div>
			</div>
			<div class="board" v-if='winner'>
				<div class='winnerO' :class='get(winner)' v-if='winner===1'></div>
				<div class='winnerX' :class='get(winner)' v-if='winner===-1'></div>
				<h1 class='winner'>WINNER!</h1>
			</div>
			<div class="board" v-if='!winner && draw'>
				<div class='winnerX x drawX' :class='get(winner)' ></div>
				<div class='winnerO o drawO' :class='get(winner)' ></div>	
				<div class="flex">
					<h1 class='winner draw'>DRAW!</h1>
					<h1 class='winner draw'>DRAW!</h1>
					<h1 class='winner draw'>DRAW!</h1>
				</div>			
				
			</div>
			<div class="restart" @click='restart'>RESTART</div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      grids: [0, 0, 0, 0, 0, 0, 0, 0, 0],
			player:1,
			winLines:[
				[0,1,2],[3,4,5],[6,7,8],
				[0,3,6],[1,4,7],[2,5,8],
				[0,4,8],[2,4,6]
			],
			winO:0,
			winX:0,
    };
	},
	created(){
		this.winO = localStorage.getItem('winO')? localStorage.getItem('winO'):0
		this.winX = localStorage.getItem('winX')? localStorage.getItem('winX'):0
	},
	computed:{
		draw(){
			return !this.grids.some(x => x === 0)
		},
		winner(){
			for(let i = 0; i < 8; i++){
				const [a,b,c] = this.winLines[i] //解構
				const sum = this.grids[a] + this.grids[b] + this.grids[c] 
				if(sum === 3) {
					this.winO ++
					localStorage.setItem('winO',this.winO)
					return 1
				}
				if(sum === -3) {
					this.winX ++
					localStorage.setItem('winX',this.winX)
					return -1
				}
			}
			return 0
		}
	},
  methods: {
		set(id){
			if (this.grids[id] !== 0) return
			if (this.winner !== 0) return
			this.$set(this.grids, id ,this.player)
			this.player = - this.player
		},
		get(num){
			if (this.winner !== 0){
				this.player = this.winner
			}
			let o = "o playO"
			let x = "x playX"
			return num === 0 ? '' : num === -1 ? x : o
		},
		restart(){
			this.player = 1
			this.grids = [0, 0, 0, 0, 0, 0, 0, 0, 0]
			this.$emit('reStart')
		}
	},
	
};
</script>

<style src='../assets/game.css' scoped></style>
