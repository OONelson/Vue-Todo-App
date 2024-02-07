<template>
	<div>
		<Todo />
	</div>
</template>

<script>
import Todo from './components/Todo.vue';
// import Popup from './components/Popup.vue';

export default {
	name: 'App',
	components: {
		Todo
	}
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	position: relative;
	/* background-color: rgb(0, 0, 0); */
	height: 100vh;
	overflow-y: hidden;
}
.Top {
	height: 20vh;
	padding-top: 2rem;
	z-index: -10;
	background-image: url('./assets/bg-desktop-dark.jpg');
}
h1 {
	color: #fff;
}
.add {
	position: absolute;
	top: 80%;
	transform: translateX(-45%);
}
.light-mode {
	background-color: #fff;
	color: grey;
}
.dark-mode {
	background-color: #000;
	color: #fff;
}
</style>
