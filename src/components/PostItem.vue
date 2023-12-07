<template>
	<div class="post">
		<div>
			<div><strong>Name: </strong>{{ post.title }}</div>
			<div><strong>Description: </strong> {{ post.description }}</div>		
		</div>
		<my-button @click="deletePost(post.id)" class="red" style="margin-left: 5px">Delete</my-button>
	</div>
</template>
<script>
import MyButton from './UI/MyButton.vue'
export default {
  components: { MyButton },
	emits: ['delete'],
	props: {
		post: {
			type: Object,
			required: true
		}
	},
	methods: {
		deletePost(id){
			this.$emit('delete', id)
		}
	}
	
}
</script>
<style>


	.post {
		border: 2px solid green;
		border-radius: 5px;
		margin-bottom: 8px;
		padding: 8px;
		/* width: 500px; */
		background: #3f7c44;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
</style>