<template>
	<div
		id="main"
		:class="{ 'light-mode': isLightMode, 'dark-mode': !isLightMode }"
	>
		<div class="Top">
			<h1>Todo App</h1>
		</div>
		<div class="button">
			<label class="switch">
				<input
					type="checkbox"
					v-model="isToggled"
					@click="toggleMode"
					@change="toggle"
				/>
				<span class="slider round"></span>
			</label>
			<p>{{ isToggled ? 'light mode' : 'dark mode' }}</p>
		</div>
		<div>
			<input
				type="text"
				class="search"
				v-model="searchTerm"
				placeholder="Search Todos..."
			/>
		</div>

		<ul>
			<li
				class="create"
				v-for="(todo, index) in filteredTodos"
				:key="index"
			>
				<input
					type="checkbox"
					class="checkbox"
				/>
				{{ todo }}
				<img
					src="../assets/icon-cross.svg"
					alt="icon-cross"
					class="cross"
					@click="deleteTodo(index)"
				/>
			</li>
		</ul>
		<form @submit.prevent="addTodo">
			<input
				type="text"
				class="add"
				v-model="add"
				placeholder="Enter Todos"
			/>
		</form>
	</div>
</template>

<script>
import { computed, ref } from 'vue';
export default {
	data() {
		return {
			add: '',
			todos: [],
			maxTodos: 6,
			isLightMode: false,
			isToggled: false,
			searchTerm: ''
		};
	},
	name: 'Todo',
	props: {},
	methods: {
		addTodo() {
			if (this.add.trim() === '') return;
			if (this.todos.length < this.maxTodos) {
				this.todos.push(this.add);
				this.add = '';
			} else {
				alert('You have reached the maximuim number of todos...');
			}
		},
		toggleMode() {
			this.isLightMode = !this.isLightMode;
			if (this.isLightMode === true) {
				const items = document.querySelectorAll('li');
				items.forEach(item => {
					item.classList.add('white');
				});
			} else {
				const items = document.querySelectorAll('li');
				items.forEach(item => {
					item.classList.remove('white');
				});
			}
		},
		toggle() {},
		deleteTodo(index) {
			this.todos.splice(index, 1);
		}
	},

	setup() {
		const searchTerm = ref('');

		const todos = ref([]);
		const filteredTodos = computed(() => {
			return todos.value.filter(todo => todo.includes(searchTerm.value));
		});

		return { todos, searchTerm, filteredTodos };
	}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
	margin: 40px 0 0;
}
ul {
	list-style-type: none;
	padding: 0;
}
li {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin: 1rem 10rem;
	padding: 0.5rem 0;
}
a {
	color: #42b983;
}
input {
	max-width: 20rem;
	width: 100%;
	padding: 0.5rem 1rem;
	font-family: Arial, Helvetica, sans-serif;
}
.search {
	position: sticky;
	margin-top: -15rem;
}
input:active {
	border-color: purple;
}
.toggle-btn {
	position: absolute;
	top: -450%;
	right: -100%;
}
.toggle-light {
	display: none;
}
.toggle-dark,
.toggle-light:hover {
	cursor: pointer;
}
.create {
	color: #fff;
	background-color: hsl(235, 21%, 11%);
	display: flex;
	justify-content: space-between;
}
.light-mode {
	background-color: #fff;
	color: grey;
}
.dark-mode {
	background-color: #000;
	color: #fff;
}
.switch {
	position: relative;
	display: inline-block;
	width: 6rem;
	height: 2.2rem;
}
.switch input {
	display: none;
}
.slider {
	position: absolute;
	cursor: pointer;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	background-color: #ccc;
	transition: 0.4s;
	border-radius: 34px;
}
.slider:before {
	position: absolute;
	content: '';
	height: 26px;
	width: 26px;
	left: 4px;
	bottom: 4px;
	background-color: #fff;
	transition: 0.4s;
	border-radius: 50%;
}
input:checked + .slider {
	background-color: #2196f3;
}
input:checked + .slider:before {
	transform: translateX(60px);
}
.slider.round {
	border-radius: 34px;
}
.slider.round:before {
	border-radius: 50%;
}
#main {
	height: 100vh;
}
.button {
	position: absolute;
	top: 5%;
	right: 5%;
}
.checkbox {
	width: max-content;
	padding: 1rem;
	margin: 0 0 0 1rem;
	cursor: pointer;
}
.add {
	margin-left: -1rem;
}
.cross {
	margin: 0 1rem 0 0;
	cursor: pointer;
}
.white {
	color: hsl(236, 44%, 13%);
	background-color: hsl(240, 2%, 69%);
}
@media screen and (max-width: 480px) {
	input {
		width: 80%;
		padding: 0.3rem 0.5rem;
	}
	li {
		margin: 1rem 5rem;
	}
	input:checked + .slider:before {
		transform: translateX(30px);
	}
	.switch {
		height: 2rem;
		width: 4rem;
	}
	.button p {
		display: none;
	}
}
@media screen and (max-width: 320px) {
	li {
		margin: 1rem 3rem;
	}
}
</style>
