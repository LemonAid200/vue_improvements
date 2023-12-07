<template>
	<div class="main">
		<my-popup v-model:show="popupVisible">
			<post-form @create="createPost"/>
		</my-popup>

		<my-button @click="openPopup" class="green" >Create new post</my-button>
		<my-select :options="sortingList" v-model="selectedSort"	class="green" style="margin-left: 10px"></my-select>

		<div style="width: fit-content; margin: 0 auto;">
			<post-list v-bind:posts="posts" @delete="deletePost"/>
		</div>

		<div v-if="loading">Loading posts...</div>
	</div>
	
</template>

<script>
import PostForm from './components/PostForm';
import PostList from './components/PostList';
import axios from 'axios';
export default {
	components: {
		PostForm, PostList
	},
	data(){
		return {
			posts: [
				// {id: 0, title: 'Post about JS', description: 'JS is the garbage I like'},
				// {id: 1, title: 'Post about Vue', description: 'Vue is actually kinda nice'},
				// {id: 2, title: 'Scooped post', description: 'I wish I was a scientist'},
			],
			popupVisible: false,
			loading: false,
			sortingList: [
				{value: 'id', name: 'id'}, 
				{value: 'title', name: 'title'}, 
				{value: 'description', name: 'description'}
			],
			selectedSort: ''
		}
	},
	methods: {
		createPost(post){
			this.posts.push(
				post
			)
			this.popupVisible = false	
		},
		deletePost(id){
			this.posts = this.posts.filter((post) => post.id != id)
		},
		openPopup(){
			this.popupVisible = true
		},
		async getPosts(){
			this.loading = true
			try {
				const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=10')
				response.data.forEach(post => {
					this.posts.push({
						id: post.id,
						title: post.title,
						description: post.body
					})
				});
			} catch (e) {
				alert('Couldn`t get posts from server')
				console.log(e)
			} finally {
				this.loading = false				
			}
		}

	},
	computed: {

	},
	watch: {
		selectedSort(newValue){
			this.posts = this.posts.sort((post_1, post_2) => {
				if (typeof post_1[newValue] === 'number') {
					console.log(post_1[newValue])
					return post_1[newValue] - post_2[newValue]
				}
				return post_1[newValue]?.toLowerCase().localeCompare(post_2[newValue].toLowerCase())
			})
		}
	},
	mounted(){
		this.getPosts()
	}
}
</script>

<style>
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	body {
		min-height: 100vh;
		background: rgb(59,191,72);
		background: linear-gradient(328deg, rgba(59,191,72,1) 0%, rgba(87,228,76,1) 27%, rgba(13,40,8,1) 100%);
		padding-bottom: 20px;
	}

	.main{
		/* width: max-content;	 */
		max-width: 600px;
		margin: auto;
		padding: 20px;
	}
</style>