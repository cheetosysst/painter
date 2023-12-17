<script setup lang="ts">
import { getHighlighter, bundledLanguagesBase, bundledThemes } from 'shikiji';
import domtoimage from "dom-to-image";

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
function getImage() {
}
function copyImage() {
	const element = document.querySelector("div#codeResult > .shiki")!;
	return domtoimage.toBlob(element).then((rawData) => {
		const type = "image/png";
		const blob = new Blob([rawData], { type });
		const data = [new ClipboardItem({ [type]: blob })];

		navigator.clipboard.write(data);
	}).catch(error => console.log(error));
}

function saveImage() {
	const element = document.querySelector("div#codeResult > .shiki")!;
	return domtoimage.toBlob(element).then((rawData) => {
		const type = "image/png";
		const blob = new Blob([rawData], { type });
		const blobURL = URL.createObjectURL(blob);

		const download = document.createElement("a");
		download.href = blobURL;
		download.download = `painter-${new Date().toISOString()}.png`;

		download.click();

		URL.revokeObjectURL(blobURL);

	}).catch(error => console.log(error));

}
</script>

<script lang="ts">

</script>

<template>
	<div class="card card-compact bg-base-200 shadow-sm">
		<div class="card-body">
			<div class="flex gap-4 flex-wrap items-center">
				<select class="select select-bordered w-40" v-model="selectedTheme">
					<option v-for="(theme, idx) in availableThemes">
						{{ theme }}
					</option>
				</select>
				<select class="select select-bordered w-40" v-model="selectedLang">
					<option v-for="(lang, idx) in availableLanguages">
						{{ lang }}
					</option>
				</select>
				<div class="flex gap-4 flex-wrap">

					<button class="btn transition-all btn-primary" v-on:click="copyRichText">Copy
						Rich Text</button>
					<button class="btn transition-all btn-info" v-on:click="copyImage">Copy
						Image</button>
					<button class="btn transition-all btn-warning" v-on:click="saveImage">Save
						Image</button>
				</div>
			</div>
			<div class="" id="codeResult" v-html="renderedCode" />
		</div>
	</div>
</template>