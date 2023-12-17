<script setup lang="ts">
import { getHighlighter, bundledLanguagesBase, bundledThemes } from 'shikiji';

const props = defineProps<{
	code: string;
}>();

const availableLanguages = Object.keys(bundledLanguagesBase);
const availableThemes = Object.keys(bundledThemes);
const highlighter = await getHighlighter({
	themes: availableThemes,
	langs: availableLanguages,
});

await highlighter.loadTheme('vitesse-light');

const selectedTheme: Ref<keyof typeof bundledThemes> = ref("material-theme-darker");
const selectedLang: Ref<keyof typeof bundledLanguagesBase> = ref("javascript");

const renderedCode = computed(() => {
	return highlighter.codeToHtml("\n" + props.code || "", {
		lang: selectedLang.value as string,
		theme: selectedTheme.value
	});
});

function copyRichText(payload: Event) {
	const element = document.querySelector("div#codeResult")!;

	const blob = new Blob([element.innerHTML], { type: "text/html" });
	const data = [new ClipboardItem({ ["text/html"]: blob })];

	navigator.clipboard.write(data);
}
</script>

<script lang="ts">

</script>

<template>
	<div class="card card-compact bg-base-200 shadow-sm">
		<div class="card-body">
			<div class="flex gap-4">
				<select class="select select-bordered w-48" v-model="selectedTheme">
					<option v-for="(theme, idx) in availableThemes">
						{{ theme }}
					</option>
				</select>
				<select class="select select-bordered w-48" v-model="selectedLang">
					<option v-for="(lang, idx) in availableLanguages">
						{{ lang }}
					</option>
				</select>
				<button class="btn btn-primary" v-on:click="copyRichText">Copy Rich Text</button>
				<button class="btn btn-info">Copy Image</button>
				<button class="btn btn-warning">Save Image</button>
			</div>
			<div class="" id="codeResult" v-html="renderedCode" />
		</div>
	</div>
</template>