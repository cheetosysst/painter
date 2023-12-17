<script setup>
import { themeChange } from "theme-change";
onMounted(() => {
	themeChange(false);
});
</script>

<template>
	<NuxtLayout>
		<NuxtPage />
	</NuxtLayout>
</template>
