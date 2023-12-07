<template >
	<div class="popup__background" v-if="show" @click="hidePopup">
		<div class="popup__content" @click.stop>
			<slot></slot>
		</div>
	</div>
</template>
<script>
export default {
	name: 'my-popup',
	props: {
		show: {
			type: Boolean,
			default: false
		},
	},
	methods: {
		hidePopup(){
			this.$emit('update:show', false)
		}
	}
}
</script>
<style scoped>
.popup__background {
	background-color: rgba(0, 0, 0, 0.8);
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	position: fixed;
	align-content: center;
	display: flex;
}
.popup__content {
	margin: auto;
	padding: 20px;
	display: flex;
	justify-content: space-around;
	background-color: white;
	border-radius: 10px;
	width: max-content;
}
</style>