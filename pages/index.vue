<script setup lang="ts">
import { ArrowRight } from "lucide-vue-next";
const route = useRoute();

const codeContent = ref<string>("");

</script>

<template>
	<div class="h-[40dvh] p-4 flex gap-2 flex-col">
		<textarea v-model="codeContent" placeholder="Paste your code here..."
			className="textarea textarea-bordered w-1/2 resize-none h-full" />
		<Highlighter :code="codeContent" />
	</div>
</template>
