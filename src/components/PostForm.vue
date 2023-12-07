<template>
		<form @submit.prevent="addPost">
		<my-input ref="firstInput" :autoFocus="true" v-model="form.title" placeholder="Title"></my-input>
		<my-input v-model="form.description" placeholder="Description"></my-input>
		<my-button class="green">Submit</my-button>
	</form>
</template>
<script>
export default {
	emits: ['create'],
	data(){
		return {
			form: {title: '', description: ''}			
			}
	},
	methods: {
		addPost(){
			if (!this.form.title || !this.form.description) return
			let post = {
				id: Date.now(),
				title: this.form.title, 
				description: this.form.description
			}
			this.$emit('create', post)

			this.form.title = ''
			this.form.description = ''
		}
	}	
}
</script>
<style scoped>
	form {
		display: flex;
		flex-direction: column;
		width: 500px;
		margin: 8px;
	}


</style>