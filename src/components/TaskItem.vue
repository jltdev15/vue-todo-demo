<template>

    <li class="flex gap-3 p-2 my-2 rounded-sm shadow">
        <input type="checkbox" @change="toggleTaskHandler">
        <p :class="{ ' line-through': props.isCompleted }">{{ props.name }} </p><button v-show="props.isCompleted"
            class="px-3 ml-auto bg-red-600 text-gray-50" @click="removeTaskHandler">Remove</button>
    </li>

</template>
<script setup>
const props = defineProps(['name', 'id', 'isCompleted'])
const emit = defineEmits(['toggleTask', 'removeTask'])

console.log(props.isCompleted)
const toggleTaskHandler = () => {
    emit('toggleTask', props.id)
}
const removeTaskHandler = () => {
    emit('removeTask', props.id)
}

</script>