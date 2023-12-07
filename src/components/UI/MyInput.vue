<template>
	<input  :value="modelValue" @input="updateInput" type="text" ref="input">
</template>
<script>
export default {
	name: 'my-input',
	emits: ['update:model-value'],
	props: {
		modelValue: [String, Number],
		autoFocus: {
			type: Boolean,
			required: false,
		}
	},
	methods: {
		updateInput(event){
			this.$emit('update:model-value', event.target.value)
		}
	},
	mounted(){
		if (this.autoFocus){
			this.$refs.input.focus()
		}
	}
}
</script>
<style scoped>
	input {
		margin-bottom: 8px;
		line-height: 16px;
		font-size: 16px;
	}	
</style>