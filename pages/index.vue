<script setup lang="ts">

const codeContent = ref<string>("");

</script>

<template>
	<div class="p-4 flex gap-8 min-h-[93dvh] flex-col">
		<div class="card bg-base-200 h-[40dvh] shadow-sm">
			<div class="card-body flex flex-col">
				<h2 class="text-3xl font-semibold">
					Source Code
				</h2>
				<textarea spellcheck="false" v-model="codeContent" placeholder="Paste your code here..."
					class="textarea textarea-bordered overflow-hidden flex-grow outline-none" />
			</div>
		</div>
		<Highlighter :code="codeContent" class="min-h-[50dvh]" />
	</div>
</template>
