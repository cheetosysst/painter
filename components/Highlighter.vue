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
	return highlighter.codeToHtml(props.code || "", {
		lang: selectedLang.value as string,
		theme: selectedTheme.value
	});
});

function themeSelect() {
	console.log(selectedTheme.value);
}
</script>

<script lang="ts">

</script>

<template>
	<div class="card card-compact bg-base-200 shadow-xl">
		<div class="card-body">
			<div class="flex gap-4">
				<select class="select select-bordered max-w-xs w-full" v-model="selectedTheme" v-on:change="themeSelect">
					<option v-for="(theme, idx) in availableThemes">
						{{ theme }}
					</option>
				</select>
				<select class="select select-bordered max-w-xs w-full" v-model="selectedLang" v-on:change="themeSelect">
					<option v-for="(lang, idx) in availableLanguages">
						{{ lang }}
					</option>
				</select>
			</div>
			<div class="" v-html="renderedCode" />
		</div>
	</div>
</template>