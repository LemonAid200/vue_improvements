<template>
	<div class="postList">
		<div v-if="posts.length === 0"><h1>No posts yet</h1></div>
		<post-item v-for="post in posts" v-bind:post="post" :key="post.id" @delete="deletePost"/>
	</div>	
</template>
<script>
import PostItem from './PostItem.vue'
export default {
	emits: ['delete'],
	components: {
		PostItem
	},
	props: {
		posts: {
			type: Array,
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
<style scoped>
.postList{
	padding-top: 8px;
}
</style>