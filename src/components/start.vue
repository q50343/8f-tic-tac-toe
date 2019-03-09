<template>
  <div class="black">
    <div class="container">
		<div class="flex">
			<div class="word">TIC</div>
			<div class="solid"><span class='o'></span></div>
			<div class="hollow">×</div>
		</div>
		<div class="flex">
			<div class="solid">×</div>
			<div class="word">TAC</div>
			<div class="solid"><span class='o hollowO'></span></div>
		</div>
		<div class="flex">				
			<div class="solid"><span class='o hollowO'></span></div>
			<div class="solid">×</div>
			<div class="word">TOE</div>
		</div>
		<div class="start" @click='start'>START</div>
	</div>
  </div>
</template>

<script>
export default {
	methods:{
		start(){
			this.$emit('start')
		}
	}
};
</script>

<style src='../assets/start.css' scoped></style>