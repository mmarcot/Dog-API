<template>
	<div class="input-group col-sm-5 mx-auto">
		<input 
			type="text" 
			class="form-control" 
			id="dog-input" 
			placeholder="Search a breed" 
			v-on:keyup.enter="searchDog"
		/>
		<div class="input-group-append">
			<button class="btn btn-success">Go !</button>
		</div>
	</div>
</template>


<script>
	export default {
		name: "DogInput",
		methods: {
			searchDog() {
				let dogInput = document.getElementById('dog-input');
				this.$emit('search-dog', { dogInputValue: dogInput.value });
				dogInput.value = '';
			}
		}
	}	
</script>


<style scoped lang="scss">
	
</style>