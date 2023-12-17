<script setup lang="ts">

const codeContent = ref<string>("");

function handleTab(payload: KeyboardEvent) {
	if (payload.key !== "Tab") return;
	payload.preventDefault();

	const textarea = payload.target as HTMLTextAreaElement;

	const selectionStart: number = textarea.selectionStart;
	const selectionEnd: number = textarea.selectionEnd;

	const textBeforeCursor = textarea.value.substring(0, selectionStart);
	const textAfterCursor = textarea.value.substring(selectionEnd);

	textarea.value = textBeforeCursor + '\t' + textAfterCursor;

	textarea.selectionStart = textarea.selectionEnd = selectionStart + 1;

}

</script>

<template>
	<div class="flex w-full p-4 gap-8 min-h-[93dvh] flex-col">
		<div class="card bg-base-200 h-[40dvh] shadow-sm">
			<div class="card-body flex flex-col">
				<h2 class="text-3xl font-semibold">
					Source Code
				</h2>
				<textarea spellcheck="false" v-model="codeContent" @keydown="handleTab"
					placeholder="Paste your code here..."
					class="textarea textarea-bordered overflow-hidden flex-grow outline-none" />
			</div>
		</div>
		<Highlighter :code="codeContent" class="min-h-[45dvh]" />
	</div>
</template>
