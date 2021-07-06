<!DOCTYPE html>
<html lang="en">
<head>
	<title></title>
	<script src="https://unpkg.com/vue/dist/vue.min.js"></script>
	<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
</head>
<body>
	
  	<div id="app">
  		<input id="search_bar" v-model="Filter_Word" @change="Filter" type="text" placeholder="input...">
  		<button v-on:click="ASC">正序</button>
  		<button v-on:click="DESC">倒序</button>

  		<table>
  			<thead>
		        <tr>
		            <th>國旗</th>
		            <th>國家名稱</th>
		            <th>2位國家代碼</th>
		            <th>3位國家代碼</th>
		            <th>母語名稱</th>
		            <th>替代國家名稱</th>
		            <th>國際電話區號</th>
		        </tr>
			</thead>
  			<tr v-for="data in info">
  				<td><img :src="data.flag" style="max-height: 20px;max-width: 40px"></td>
  				<td>{{data.name}}</td>
  				<td>{{data.alpha2Code}}</td>
  				<td>{{data.alpha3Code}}</td>
  				<td>{{data.nativeName}}</td>
  				<td>{{data.altSpellings}}</td>
  				<td>{{data.callingCodes}}</td>
  			</tr>
  			
  		</table>
  	</div>
  	
</body>
<script>

	new Vue({
	  	el: '#app',
	  	data () {
	    	return {
	      		info: null,
	      		Filter_Word: ""
	    	}
	  	},
	  	mounted () {
	    	axios
	      	.get('https://restcountries.eu/rest/v2/all')
	      	.then(response => {
	      		this.info = response.data;
	      	})
	  	},
		methods: {
			ASC: function (event) {
			    	axios
			      	.get('https://restcountries.eu/rest/v2/all')
			      	.then(response => {
			      			this.info = response.data.sort();
			      	})
		  	},
		  	DESC: function (event) {
			    	axios
			      	.get('https://restcountries.eu/rest/v2/all')
			      	.then(response => {
			      		this.info = response.data.reverse();
			      	})
		  	},
		  	Filter: function (event) {
			    	axios
			      	.get('https://restcountries.eu/rest/v2/all')
			      	.then(response => {
			      		var tmp = response.data;
			      		this.info = tmp.filter(data => data.name.includes(this.Filter_Word))
			      	})
		  	}
		}

	})
</script>
</html>
