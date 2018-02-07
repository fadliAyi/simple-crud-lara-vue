<template>
	<div>
		<div class="form-group">
			<router-link to="/" class="btn btn-default"> Back </router-link>	
		</div>	
		<div class="panel panel-default">
			<div class="panel-heading"> Create New Company </div>
			<div class="panel-body">
				<form v-on:submit="saveForm()">
					<div class="row">
						<div class="row-xs-12 form-group">
							<label class="control-label"> Company Name </label>
							<input class="form-control" type="text" v-model="company.name">	
						</div>
					</div>	
					<div class="row">
						<div class="row-xs-12 form-group">
							<label class="control-label"> Company Address</label>
							<input class="form-control" type="text" v-model="company.address">	
						</div>
					</div>
					<div class="row">
						<div class="row-xs-12 form-group">
							<label class="control-label"> Company Website </label>
							<input class="form-control" type="text" v-model="company.website">	
						</div>
					</div>
					<div class="row">
						<div class="row-xs-12 form-group">
							<label class="control-label"> Company Email </label>
							<input class="form-control" type="text" v-model="company.email">	
						</div>
					</div>
					<div class="row">
						<div class="row-xs-12 form-group">
							<button class="btn btn-success">Create</button>
						</div>
					</div>
				</form>	
			</div>
		</div>
	</div>	
</template>

<script>
	export default{
		data: function () {
			return {
				company: {
					name:'',
					address: '',
					website: '',
					email: ''	
				}	
			}	
		},
	methods:{
		saveForm(){
			event.preventDefault();	
			var app = this;
			var newCompany = app.company;	
			axios.post('/api/v1/companies', newCompany)
					.then(function(resp){
						app.$router.push({ path: '/' });	
					})
					.catch(function(resp){
						console.log(resp);
						alert("Could not create company");	
					});
		}	
	}	
	}	
</script>