<template>
	<button @click="() => this.$emit('click')">		
		<slot></slot>
	</button>
</template>
<script>
export default {
	name: 'my-button',
	emits: ['click']
}
</script>
<style scoped>
	button{
    padding: 5px;
    border: 2px solid ;
    border-radius: 5px;
    font-size: 13px;
    line-height: 13px;
		cursor: pointer;
		height: 30px;
	}

	.red{
    border-color: rgb(171 0 0);
    background: #ffffff61;
    color: rgb(171 0 0);
	}

	.green{
		border-color: rgb(6, 171, 0);
    background: rgba(255, 255, 255, 0.973);
    color: rgb(0, 171, 0);
	}
	
</style>