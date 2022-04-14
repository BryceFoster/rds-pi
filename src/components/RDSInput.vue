<template>
	<form @submit="submitPi">
		<div class="form-control">
			<input type="text" v-model="piCode" placeholder="Input PI Code" />
			<input type="submit" value="Submit" />
		</div>
	</form>
</template>

<script>
export default {
	name: 'RDSInput',
	data() {
		return {
			piCode: ""
		}
	},
	methods: {
		submitPi(e) {
			e.preventDefault()
			const pi = this.piCode
			this.$emit('lookup-pi', pi)
			this.piCode = ''
		}
	}
}
</script>

<style scoped>
.add-form {
	margin-bottom: 40px,
}
.form-control {
	margin: 20px 0;
}
.form-control label {
	display: block;
}
.form-control input {
	width: 100%;
	height: 40px;
	margin: 5px;
	padding: 3px 7px;
	font-size: 17px;
}
.form-control-check {
	display: flex;
	align-items: center;
	justify-content: space-between;
}
.form-control-check label {
	flex: 1;
}
.form-control-check input {
	flex: 2;
	height: 20px;
}
</style>