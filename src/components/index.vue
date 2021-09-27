<template>
	<p>{{ props.msg }}</p>
	<button @click="handleClick">点击调用父</button>
	<p>count: {{ count }}</p>
	<button @click="increment">+</button>
	<button @click="count--">-</button>
	<p>name: {{ user.name }}, age: {{ user.age }}</p>
	<button @click="userAgeAdd">add age</button>
	<button
		@click="
			() => {
				user.name = user.name !== '张三' ? '张三' : '李四';
			}
		"
	>
		name change
	</button>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue';

const count = ref(0);
const user = reactive({ name: '张三', age: 18 });

const increment = () => {
	count.value++;
	console.log('increment count ++, count:', count.value);
};

const userAgeAdd = () => {
	user.age++;
};

const props = defineProps({
	msg: {
		type: String,
		default: '默认信息',
	},
});
const emit = defineEmits(['on-change']);
const handleClick = () => {
	emit('on-change', '点击父组件调用');
};

const childNode = () => {
	console.log('子组件方法被调用');
};

defineExpose({
	child: '子组件暴露',
	childNode,
});
</script>

<style lang="scss" scoped></style>
