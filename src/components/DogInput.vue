<template>
	<input 
		type="text" 
		class="form-control w-50 mx-auto" 
		id="dog-input" 
		placeholder="Search" 
		v-on:keyup.enter="searchDog"
	/>
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