<template>
	<div class="container-fluid p-0" id="app">
		<div class="jumbotron py-1">
			<h1 class="display-5">DogAPI</h1>
		</div>
		<div class="input-group col-sm-5 mx-auto">
			<Autocomplete 
				id="autocompleteTag"
				:source="inputList" 
				inputClass="form-control"
				@selected="onBreedSelected"
				placeholder="Search breed"
			></Autocomplete>
		</div>
	<button class="btn btn-info my-4" v-on:click="randomDog">Random</button>
	<img id="dog-image" class="d-block mx-auto" v-bind:src="imgSource">
</div>
</template>

<script>
	import Autocomplete from 'vuejs-auto-complete'

	export default {
		name: 'App',
		data() {
			let idVar = 0;
			return {
				imgSource: '',
				inputList: [
					{id:idVar++, idName: "affenpinscher", name: "Affenpinscher"},
					{id:idVar++, idName: "hound/afghan", name: "Afghan Hound"},
					{id:idVar++, idName: "african", name: "African"},
					{id:idVar++, idName: "airedale", name: "Airedale"},
					{id:idVar++, idName: "akita", name: "Akita"},
					{id:idVar++, idName: "terrier/american", name: "American Terrier"},
					{id:idVar++, idName: "appenzeller", name: "Appenzeller"},
					{id:idVar++, idName: "cattledog/australian", name: "Australian Cattledog"},
					{id:idVar++, idName: "terrier/australian", name: "Australian Terrier"},
					{id:idVar++, idName: "basenji", name: "Basenji"},
					{id:idVar++, idName: "hound/basset", name: "Basset Hound"},
					{id:idVar++, idName: "beagle", name: "Beagle"},
					{id:idVar++, idName: "terrier/bedlington", name: "Bedlington Terrier"},
					{id:idVar++, idName: "mountain/bernese", name: "Bernese Mountain"},
					{id:idVar++, idName: "frise/bichon", name: "Bichon Frise"},
					{id:idVar++, idName: "spaniel/blenheim", name: "Blenheim Spaniel"},
					{id:idVar++, idName: "hound/blood", name: "Blood Hound"},
					{id:idVar++, idName: "bluetick", name: "Bluetick"},
					{id:idVar++, idName: "collie/border", name: "Border Collie"},
					{id:idVar++, idName: "terrier/border", name: "Border Terrier"},
					{id:idVar++, idName: "borzoi", name: "Borzoi"},
					{id:idVar++, idName: "bulldog/boston", name: "Boston Bulldog"},
					{id:idVar++, idName: "bouvier", name: "Bouvier"},
					{id:idVar++, idName: "boxer", name: "Boxer"},
					{id:idVar++, idName: "brabancon", name: "Brabancon"},
					{id:idVar++, idName: "briard", name: "Briard"},
					{id:idVar++, idName: "spaniel/brittany", name: "Brittany Spaniel"},
					{id:idVar++, idName: "mastiff/bull", name: "Bull Mastiff"},
					{id:idVar++, idName: "cairn", name: "Cairn"},
					{id:idVar++, idName: "corgi/cardigan", name: "Cardigan Corgi"},
					{id:idVar++, idName: "ovcharka/caucasian", name: "Caucasian Ovcharka"},
					{id:idVar++, idName: "retriever/chesapeake", name: "Chesapeake Retriever"},
					{id:idVar++, idName: "chihuahua", name: "Chihuahua"},
					{id:idVar++, idName: "chow", name: "Chow"},
					{id:idVar++, idName: "clumber", name: "Clumber"},
					{id:idVar++, idName: "cockapoo", name: "Cockapoo"},
					{id:idVar++, idName: "spaniel/cocker", name: "Cocker Spaniel"},
					{id:idVar++, idName: "coonhound", name: "Coonhound"},
					{id:idVar++, idName: "cotondetulear", name: "Cotondetulear"},
					{id:idVar++, idName: "retriever/curly", name: "Curly Retriever"},
					{id:idVar++, idName: "dachshund", name: "Dachshund"},
					{id:idVar++, idName: "dalmatian", name: "Dalmatian"},
					{id:idVar++, idName: "terrier/dandie", name: "Dandie Terrier"},
					{id:idVar++, idName: "dhole", name: "Dhole"},
					{id:idVar++, idName: "dingo", name: "Dingo"},
					{id:idVar++, idName: "doberman", name: "Doberman"},
					{id:idVar++, idName: "bulldog/english", name: "English Bulldog"},
					{id:idVar++, idName: "hound/english", name: "English Hound"},
					{id:idVar++, idName: "mastiff/english", name: "English Mastiff"},
					{id:idVar++, idName: "setter/english", name: "English Setter"},
					{id:idVar++, idName: "sheepdog/english", name: "English Sheepdog"},
					{id:idVar++, idName: "springer/english", name: "English Springer"},
					{id:idVar++, idName: "entlebucher", name: "Entlebucher"},
					{id:idVar++, idName: "eskimo", name: "Eskimo"},
					{id:idVar++, idName: "retriever/flatcoated", name: "Flatcoated Retriever"},
					{id:idVar++, idName: "terrier/fox", name: "Fox Terrier"},
					{id:idVar++, idName: "bulldog/french", name: "French Bulldog"},
					{id:idVar++, idName: "pointer/german", name: "German Pointer"},
					{id:idVar++, idName: "pointer/germanlonghair", name: "Germanlonghair Pointer"},
					{id:idVar++, idName: "germanshepherd", name: "Germanshepherd"},
					{id:idVar++, idName: "schnauzer/giant", name: "Giant Schnauzer"},
					{id:idVar++, idName: "retriever/golden", name: "Golden Retriever"},
					{id:idVar++, idName: "setter/gordon", name: "Gordon Setter"},
					{id:idVar++, idName: "dane/great", name: "Great Dane"},
					{id:idVar++, idName: "groenendael", name: "Groenendael"},
					{id:idVar++, idName: "havanese", name: "Havanese"},
					{id:idVar++, idName: "husky", name: "Husky"},
					{id:idVar++, idName: "hound/ibizan", name: "Ibizan Hound"},
					{id:idVar++, idName: "setter/irish", name: "Irish Setter"},
					{id:idVar++, idName: "spaniel/irish", name: "Irish Spaniel"},
					{id:idVar++, idName: "terrier/irish", name: "Irish Terrier"},
					{id:idVar++, idName: "wolfhound/irish", name: "Irish Wolfhound"},
					{id:idVar++, idName: "greyhound/italian", name: "Italian Greyhound"},
					{id:idVar++, idName: "spaniel/japanese", name: "Japanese Spaniel"},
					{id:idVar++, idName: "keeshond", name: "Keeshond"},
					{id:idVar++, idName: "kelpie", name: "Kelpie"},
					{id:idVar++, idName: "terrier/kerryblue", name: "Kerryblue Terrier"},
					{id:idVar++, idName: "komondor", name: "Komondor"},
					{id:idVar++, idName: "kuvasz", name: "Kuvasz"},
					{id:idVar++, idName: "labrador", name: "Labrador"},
					{id:idVar++, idName: "terrier/lakeland", name: "Lakeland Terrier"},
					{id:idVar++, idName: "finnish/lapphund", name: "Lapphund Finnish"},
					{id:idVar++, idName: "leonberg", name: "Leonberg"},
					{id:idVar++, idName: "lhasa", name: "Lhasa"},
					{id:idVar++, idName: "malamute", name: "Malamute"},
					{id:idVar++, idName: "malinois", name: "Malinois"},
					{id:idVar++, idName: "maltese", name: "Maltese"},
					{id:idVar++, idName: "mexicanhairless", name: "Mexicanhairless"},
					{id:idVar++, idName: "pinscher/miniature", name: "Miniature Pinscher"},
					{id:idVar++, idName: "poodle/miniature", name: "Miniature Poodle"},
					{id:idVar++, idName: "schnauzer/miniature", name: "Miniature Schnauzer"},
					{id:idVar++, idName: "mix", name: "Mix"},
					{id:idVar++, idName: "newfoundland", name: "Newfoundland"},
					{id:idVar++, idName: "terrier/norfolk", name: "Norfolk Terrier"},
					{id:idVar++, idName: "buhund/norwegian", name: "Norwegian Buhund"},
					{id:idVar++, idName: "elkhound/norwegian", name: "Norwegian Elkhound"},
					{id:idVar++, idName: "terrier/norwich", name: "Norwich Terrier"},
					{id:idVar++, idName: "otterhound", name: "Otterhound"},
					{id:idVar++, idName: "papillon", name: "Papillon"},
					{id:idVar++, idName: "terrier/patterdale", name: "Patterdale Terrier"},
					{id:idVar++, idName: "pekinese", name: "Pekinese"},
					{id:idVar++, idName: "pembroke", name: "Pembroke"},
					{id:idVar++, idName: "pitbull", name: "Pitbull"},
					{id:idVar++, idName: "hound/plott", name: "Plott Hound"},
					{id:idVar++, idName: "pomeranian", name: "Pomeranian"},
					{id:idVar++, idName: "puggle", name: "Puggle"},
					{id:idVar++, idName: "pug", name: "Pug"},
					{id:idVar++, idName: "pyrenees", name: "Pyrenees"},
					{id:idVar++, idName: "redbone", name: "Redbone"},
					{id:idVar++, idName: "ridgeback/rhodesian", name: "Rhodesian Ridgeback"},
					{id:idVar++, idName: "rottweiler", name: "Rottweiler"},
					{id:idVar++, idName: "terrier/russell", name: "Russell Terrier"},
					{id:idVar++, idName: "saluki", name: "Saluki"},
					{id:idVar++, idName: "samoyed", name: "Samoyed"},
					{id:idVar++, idName: "schipperke", name: "Schipperke"},
					{id:idVar++, idName: "deerhound/scottish", name: "Scottish Deerhound"},
					{id:idVar++, idName: "terrier/scottish", name: "Scottish Terrier"},
					{id:idVar++, idName: "terrier/sealyham", name: "Sealyham Terrier"},
					{id:idVar++, idName: "australian/shepherd", name: "Shepherd Australian"},
					{id:idVar++, idName: "sheepdog/shetland", name: "Shetland Sheepdog"},
					{id:idVar++, idName: "shiba", name: "Shiba"},
					{id:idVar++, idName: "shihtzu", name: "Shihtzu"},
					{id:idVar++, idName: "terrier/silky", name: "Silky Terrier"},
					{id:idVar++, idName: "waterdog/spanish", name: "Spanish Waterdog"},
					{id:idVar++, idName: "bullterrier/staffordshire", name: "Staffordshire Bullterrier"},
					{id:idVar++, idName: "poodle/standard", name: "Standard Poodle"},
					{id:idVar++, idName: "stbernard", name: "Stbernard"},
					{id:idVar++, idName: "spaniel/sussex", name: "Sussex Spaniel"},
					{id:idVar++, idName: "mountain/swiss", name: "Swiss Mountain"},
					{id:idVar++, idName: "mastiff/tibetan", name: "Tibetan Mastiff"},
					{id:idVar++, idName: "terrier/tibetan", name: "Tibetan Terrier"},
					{id:idVar++, idName: "poodle/toy", name: "Toy Poodle"},
					{id:idVar++, idName: "terrier/toy", name: "Toy Terrier"},
					{id:idVar++, idName: "vizsla", name: "Vizsla"},
					{id:idVar++, idName: "hound/walker", name: "Walker Hound"},
					{id:idVar++, idName: "weimaraner", name: "Weimaraner"},
					{id:idVar++, idName: "spaniel/welsh", name: "Welsh Spaniel"},
					{id:idVar++, idName: "terrier/westhighland", name: "Westhighland Terrier"},
					{id:idVar++, idName: "terrier/wheaten", name: "Wheaten Terrier"},
					{id:idVar++, idName: "whippet", name: "Whippet"},
					{id:idVar++, idName: "terrier/yorkshire", name: "Yorkshire Terrier"},

				]
			}
		},
		components: {
			Autocomplete
		},
		methods: {
			onBreedSelected(payload) {
				var xhttp = new XMLHttpRequest();
				let this_comp = this;
				xhttp.onreadystatechange = function() {
					if (this.readyState == XMLHttpRequest.DONE && this.status == 200) {
						var response = JSON.parse(this.responseText);
						this_comp.imgSource = response.message;
					}
				};
				let res;
				for (var i = this.inputList.length - 1; i >= 0; i--) {
					if (this.inputList[i].id == payload.selectedObject.id) {
						res = this.inputList[i];
						break;
					}
				}
				xhttp.open('GET', 'https://dog.ceo/api/breed/' + res.idName.replace(' ', '-') + '/images/random');
				xhttp.send();
			},
			randomDog() {
				document.getElementById('autocompleteTag').resultsValue = '';
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
