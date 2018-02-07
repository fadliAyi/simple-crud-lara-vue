<template>
	<div>
		<div class="form-group">
			<router-link :to="{name: 'createCompany'}"	class="btn btn-success">Create New Company </router-link> 
		</div>	

		<div class="panel panel-default">
			<div class="panel-heading"> Company List</div>
			<div class="panel-body">
				<table class="table table-bordered table-sriped">
					<thead>
						<tr>
							<th>Name</th>
							<th>Address</th>
							<th>Website</th>
							<th>email</th>
							<th>action</th>
						</tr>
					</thead>	
					<tbody>
						<tr v-for="(company, index) in companies">
							<td>{{ company.name }}</td>	
							<td>{{ company.address }}</td>	
							<td>{{ company.website}}</td>	
							<td>{{ company.email }}</td>	
							<td>
								<router-link :to="{name: 'editCompany', params:{id: company.id}}"	class="btn  btn-xs btn-default">Edit 
								</router-link> 
								<a href="#" class="btn btn-xs btn-danger" v-on:click= "deleteEndtry(company.id, index)"> delete </a>
							</td>
						</tr>	
					</tbody>
				</table>	
			</div>
		</div>	
	</div>	
</template>

<script>
	export default {
		data: function () {
			return {
				companies: []
			} 
		},
		mounted(){
			var app = this;
			axios.get('/api/v1/companies')
			.then(function(resp){
				console.log(resp.data);
				app.companies = resp.data;	
			}).catch(function(resp) {
				console.log(resp);
				console.log(resp.data);
				alert("could not loaded companies");
			});	
		},
		methods: {
			deleteEndtry(id, index){
				if (confirm("do you really want to delete this?")) {
					var app = this;
					axios.delete('/api/v1/companies/' + id).
					then(function (reps) {
						app.companies.splice(index, 1);
					}).
					catch(function (resp) {
						alert("cannot delete companies");
					});
				}	
			}	
		} 
	}	
</script>