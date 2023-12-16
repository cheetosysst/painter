<script setup lang="ts">
const route = useRoute();

const count = ref<number>(1);


definePageMeta({
	layout: "default"
});
</script>

<template>
	<div>
		<h1>Nuxt Routing set up successfully!</h1>
		<p>Current route: {{ route.path }}</p>
		<span>{{ count }}</span>
		<button type="button" @click="count = count + 1">click</button>

	</div>
</template>
