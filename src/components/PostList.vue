<template>
	<div v-if="posts.length === 0"><h1>No posts yet</h1></div>
	<transition-group name="post-list" tag="p" class="postList">
	<!-- <div class="postList"> -->
		<post-item v-for="post in posts" v-bind:post="post" :key="post.id" @delete="deletePost"/>
	<!-- </div> -->
</transition-group>
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

.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active, .post-list-leave-active {
  transition: all 0.5s;
}
.post-list-enter, .post-list-leave-to /* .list-leave-active до версии 2.1.8 */ {
  opacity: 0;
  transform: translateX(30px);
}
</style>