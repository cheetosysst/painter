<script setup lang="ts">

const codeContent = ref<string>("");

</script>

<template>
	<div class="p-4 flex gap-8 min-h-[93dvh] flex-col">
		<div class="card bg-base-200 flex-grow shadow-sm">
			<div class="card-body flex flex-col">
				<h2 class="text-3xl font-semibold">
					Source Code
				</h2>
				<textarea spellcheck="false" v-model="codeContent" placeholder="Paste your code here..."
					class="textarea textarea-bordered flex-grow outline-none" />
			</div>
		</div>
		<Highlighter :code="codeContent" class="flex-grow h-full" />
	</div>
</template>
