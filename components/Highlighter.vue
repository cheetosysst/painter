<script setup lang="ts">
import { watch } from "vue";
import { bundledLanguagesBase, bundledThemes, createHighlighter } from "shiki";
import domtoimage from "dom-to-image";

const props = defineProps<{
	code: string;
}>();

const availableLanguages = Object.keys(bundledLanguagesBase);
const availableThemes = Object.keys(bundledThemes);

type Themes = keyof typeof bundledThemes;
type Languages = keyof typeof bundledLanguagesBase; // TODO find a better source

const DEFAULT_THEME = "material-theme-darker";
const DEFAULT_LANG = "javascript";

const currentTheme = ref<Themes>(DEFAULT_THEME);
const currentLanguage = ref<Languages>(DEFAULT_LANG);
const cachedThemes = ref<Array<Themes>>([DEFAULT_THEME]);
const cachedLanguages = ref<Array<Languages>>([DEFAULT_LANG]);

const highlighter = ref<Awaited<ReturnType<typeof createHighlighter>> | null>(
	null
);

const renderedCode = ref<string>("");

async function updateHightlighter() {
	const newHighlighter = await createHighlighter({
		langs: cachedLanguages.value as Array<string>,
		themes: cachedThemes.value,
	});
	highlighter.value = newHighlighter;
}

function updateContent() {
	const codeToHtml = highlighter.value?.codeToHtml;
	if (codeToHtml == null) return;
	const code = codeToHtml(`\n${props.code}`, {
		theme: currentTheme.value,
		lang: currentLanguage.value as string,
	});
	renderedCode.value = code;
}

watch(
	() => currentLanguage.value,
	async (next, _) => {
		if (!cachedLanguages.value.includes(next)) {
			cachedLanguages.value.push(next);
			await updateHightlighter();
		}
		updateContent();
	}
);

watch(
	() => currentTheme.value,
	async (next, _) => {
		if (!cachedThemes.value.includes(next)) {
			cachedThemes.value.push(next);
			await updateHightlighter();
		}
		updateContent();
	}
);

watch(
	() => props.code,
	async () => {
		if (highlighter.value == null) {
			await updateHightlighter();
		}
		updateContent();
	}
);

function copyRichText(payload: Event) {
	const element = document.querySelector("pre#codeResult")!;

	const blob = new Blob([element.innerHTML], { type: "text/html" });
	const data = [new ClipboardItem({ ["text/html"]: blob })];

	navigator.clipboard.write(data);
}

function copyImage() {
	const element = document.querySelector("pre#codeResult")!;
	return domtoimage
		.toBlob(element)
		.then((rawData) => {
			const type = "image/png";
			const blob = new Blob([rawData], { type });
			const data = [new ClipboardItem({ [type]: blob })];

			navigator.clipboard.write(data);
		})
		.catch((error) => console.error(error));
}

function saveImage() {
	const element = document.querySelector("pre#codeResult")!;
	return domtoimage
		.toBlob(element)
		.then((rawData) => {
			const type = "image/png";
			const blob = new Blob([rawData], { type });
			const blobURL = URL.createObjectURL(blob);

			const download = document.createElement("a");
			download.href = blobURL;
			download.download = `painter-${new Date().toISOString()}.png`;

			download.click();

			URL.revokeObjectURL(blobURL);
		})
		.catch((error) => console.error(error));
}
</script>

<template>
	<div class="card card-compact bg-base-200 shadow-sm">
		<div class="card-body">
			<div class="flex gap-4 flex-wrap items-center">
				<label for="selectTheme hidden">select theme</label>
				<select
					id="selectTheme"
					class="select select-bordered w-40"
					v-model="currentTheme"
				>
					<option v-for="theme in availableThemes" :key="theme">
						{{ theme }}
					</option>
				</select>

				<label for="selectLang hidden">select language</label>
				<select
					id="selectLang"
					class="select select-bordered w-40"
					v-model="currentLanguage"
				>
					<option v-for="lang in availableLanguages" :key="lang">
						{{ lang }}
					</option>
				</select>

				<div class="flex gap-4 flex-wrap">
					<button
						class="btn transition-all btn-primary"
						v-on:click="copyRichText"
					>
						Copy Rich Text
					</button>
					<button
						class="btn transition-all btn-info"
						v-on:click="copyImage"
					>
						Copy Image
					</button>
					<button
						class="btn transition-all btn-warning"
						v-on:click="saveImage"
					>
						Save Image
					</button>
				</div>
			</div>
			<pre id="codeResult">
				<code  v-html="renderedCode"></code>
			</pre>
		</div>
	</div>
</template>
