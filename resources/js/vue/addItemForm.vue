<template>
	<div class="addItem">
		<input type="text" name="" v-model="item.name" />
		<font-awesome-icon 
		icon="plus-square"
		@click="addItem()"
		:class="[item.name ? 'active' : 'inactine' , 'plus']"
		/>
	</div>
</template>
<script>
	export default {
		data: function(){
			return {
				item: {
					name: ""
				}
			}
		},
		methods: {
			addItem() {
				if(this.item == "") {
					return ;
				}
				axios.post('api/item/store', {
					item: this.item
				})
				.then(response => {
					if(response.status == 201){
						this.item.name == "";
						this.$emit('reloadList');
					}
				})
				.catch(error=> {
					console.log(error);
				})
			}
		}
	}
</script>

<style scoped>
	.addItem {
		display:  flex;
		justify-content: center;
		align-items: center;
	}
	input {
		background: #f7f7f7;
		border: 0px;
		outline: none;
		padding: none;
		margin-right: 10px;
		width: 100%;
	}
	.plus {
		font-size: 20px;
	}

	.active {
		color:  #00CE25;
	}
	.inactive {
		color: #999999;
	}
</style>