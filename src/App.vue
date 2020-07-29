<template>
	<div class="container-fluid p-0" id="app">
		<div class="jumbotron py-1">
			<h1 class="display-5">DogAPI</h1>
		</div>
		<DogInput v-on:search-dog="searchDog" />
		<button class="btn btn-info my-4" v-on:click="randomDog">Random</button>
		<img id="dog-image" class="d-block mx-auto" v-bind:src="imgSource">
	</div>
</template>

<script>
	import DogInput from './components/DogInput.vue'

	export default {
		name: 'App',
		data() {
			return {
				imgSource: ''
			}
		},
		components: {
			DogInput
		},
		methods: {
			searchDog(payload) {
				console.log(payload.dogInputValue);
			},
			randomDog() {
				var xhttp = new XMLHttpRequest();
				let this_comp = this;
				xhttp.onreadystatechange = function() {
					if (this.readyState == XMLHttpRequest.DONE && this.status == 200) {
						var response = JSON.parse(this.responseText);
						this_comp.imgSource = response.message;
					}
				};
				xhttp.open('GET', 'https://dog.ceo/api/breeds/image/random');
				xhttp.send();
			}
		}
	}
</script>

<style lang="scss">
	#app {
		text-align: center;
	}
	#dog-image {
		max-height: 700px;
		max-width: 700px;
		height: auto;
		width: auto;
	}
</style>
