<script setup lang="ts">
import { ref } from 'vue'
import { Person } from './Persons.vue'

type Props = {
	persons: Person[]
}

defineProps<Props>()

const emit = defineEmits(['delete'])

const isDialogOpen = ref<boolean>(false)

const onClickDelete  = (id: number, name: string) => {
	isDialogOpen.value = !isDialogOpen.value

	if (confirm('Delete ' + name + '?')) {
		emit('delete', id)
	}
}
</script>

<template>
	<li v-for="person in persons" :key="person.id" class="person-list">
		<span>{{ person.name }}</span>
		<span>age:{{ person.age }}</span>
		<button @click="onClickDelete(person.id, person.name)">
			<span>delete</span>
		</button>
		<teleport to="body">
			<dialog :open="isDialogOpen" class="dialog">
				<span>Dialog</span>
			</dialog>
		</teleport>
	</li>
</template>

<style scoped>
.person-list {
	list-style: none;
	margin-bottom: 12px;
	border-radius: 4px;
	font-size: 20px;
	font-weight: bold;
	display: flex;
	justify-content: space-between;
	background-color: rgb(228, 201, 133);
	padding: 8px 20px;
	width: 300px;
}

.dialog {
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	height: 300px;
	width: 400px;
	margin: auto;
	background-color: aliceblue;
}
</style>
