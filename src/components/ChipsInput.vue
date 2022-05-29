<template>
	<div class="tag-input">
		<div v-for="(tag, index) in tags" :key="index" class="tag-input__tag">
			<span class="tag-input__tag-name">{{ tag }}</span>
			<span @click="deleteTag(index)">x</span>
		</div>
		<input
			type="text"
			placeholder="Enter a Tag"
			class="tag-input__text"
			@keypress.enter="addTag"
			@keypress.tab="addTag"
			@keypress="addTagSpace"
			@keydown.delete="removeLastTag"
		/>
	</div>
</template>
<script>
export default {
	data() {
		return {
			tags: ["hello", "world"],
		};
	},
	methods: {
		addTag(event) {
			const val = event.target.value.trim();
			this.tags.push(val);
			event.target.value = "";
		},
		addTagSpace(event) {
			if (event.keyCode === 44) {
				const val = event.target.value.trim();
				this.tags.push(val);
				event.target.value = event.target.value.split(",");
				event.target.value = "";
				event.target.value = "";
			}
		},
		removeLastTag(event) {
			if (event.target.value.length === 0) {
				this.deleteTag(this.tags.length - 1);
			}
		},
		deleteTag(index) {
			this.tags.splice(index, 1);
		},
	},
};
</script>
<style scoped>
.tag-input {
	width: 80%;
	height: auto;
	border: 0.2rem solid #dddddd;
	transition: 0.3s ease-in-out;
	font-size: 0.9em;
	min-height: 50px;
	padding: 1vh;
	border-radius: 0.2rem;
}

.tag-input__tag {
	display: flex;
	justify-content: space-around;
	align-items: center;
	height: auto;
	float: left;
	margin-right: 1vh;
	background-color: #c7ece3;
	margin-top: 0.8vh;
	line-height: 30px;
	border-radius: 5px;
	transition: 0.3s ease-in-out;
}

.tag-input__tag > span {
	cursor: pointer;
	opacity: 0.75;
	color: #4a4a4a;
	font-weight: 600;
	margin-right: 0.8vh;
	padding: 0.5vh;
}

.tag-input__tag-name {
	font-weight: 600;
	padding: 0.5vh;
	margin-right: 0.5vh;
	margin-left: 0.5vh;
	font-size: 0.8rem;
}

.tag-input__text {
	display: flex;
	justify-content: flex-start center;
	align-items: center;
	border: none;
	outline: none;
	font-size: 0.9em;
	line-height: 50px;
	background: none;
	font-size: 1rem;
}
</style>