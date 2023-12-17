<script setup lang="ts">
import { Menu, ChevronDown } from "lucide-vue-next";

useHead({
	htmlAttrs: {
		lang: "zh-TW"
	}
});

useSeoMeta({
	colorScheme: "light dark",
	applicationName: "Painter",
	author: "Chen",
	robots: "index, follow",
	googlebotNews: "noindex",

	ogType: "website",
	ogDeterminer: "the",
	ogSiteName: "Painter"
});

const themes = [
	"light",
	"dark",
	"cupcake",
	"bumblebee",
	"emerald",
	"corporate",
	"synthwave",
	"retro",
	"cyberpunk",
	"valentine",
	"halloween",
	"garden",
	"forest",
	"aqua",
	"lofi",
	"pastel",
	"fantasy",
	"wireframe",
	"black",
	"luxury",
	"dracula",
	"cmyk",
	"autumn",
	"business",
	"acid",
	"lemonade",
	"night",
	"coffee",
	"winter",
	"dim",
	"nord",
	"sunset",
]

</script>

<template>
	<div class="drawer">
		<input id="my-drawer" type="checkbox" class="drawer-toggle" />
		<div class="drawer-content min-h-[100dvh] h-fit flex flex-col">
			<!-- navbar -->
			<div class="navbar h-[6dvh] bg-base-100">
				<div class="flex-none">
					<label for="my-drawer" class="btn btn-square btn-ghost drawer-button">
						<Menu />
					</label>
				</div>
				<div class="flex-1 flex gap-2 items-baseline">
					<a href="/" class="text-3xl btn btn-ghost">
						PAINTER
					</a>
					<span class="hidden md:inline-block">Placeholder for funny sentences that makes no sense</span>
				</div>
				<div class="flex-none items-baseline">
					<div class="dropdown dropdown-end">
						<div tabindex="0" role="button" class="btn flex gap-2 items-center font-normal m-1">
							Theme
							<ChevronDown />
						</div>
						<ul tabindex="0"
							class="dropdown-content h-96 overflow-y-scroll z-[1] p-2 shadow-2xl bg-base-300 rounded-box w-fit">
							<li v-for="theme in themes"><input type="radio" name="theme-dropdown"
									class="theme-controller btn btn-sm btn-block btn-ghost justify-start"
									:aria-label="theme" :value="theme" /></li>


						</ul>
					</div>
				</div>
			</div>
			<!-- navbarend -->

			<slot />

		</div>
		<div class="drawer-side">
			<label for="my-drawer" aria-label="close sidebar" class="drawer-overlay"></label>
			<ul class="menu p-4 w-80 min-h-full bg-base-200 text-base-content">
				<li><a href="https://github.com/cheetosysst/painter">Github</a></li>
				<li><a href="/about">About</a></li>

			</ul>
		</div>
	</div>
</template>