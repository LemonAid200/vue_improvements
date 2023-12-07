<template>
	<select :value="modelValue" @change="changeOption">
		<option disabled selected value="">Sorting param</option>
		<option v-for="option in options" :value="option.value" :key="option.value">{{ option.name }}</option>
	</select>
</template>
<script>
export default {
	name: 'my-select',
	props: {
		modelValue: {
			type: String
		},
		options: {
			type: Array,
			required: true,
			default: () => [],
		}
	},
	methods: {
		changeOption(event){
			this.$emit('update:model-value', event.target.value)
			this.$nextTick(() => 
			console.log(this.modelValue)
			)
		}
	}
	
}
</script>
<style>
	select{
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
    background: #ffffffe8;
    color: rgb(0, 171, 0);
	}
</style>