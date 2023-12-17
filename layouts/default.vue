<script setup lang="ts">
import { Menu } from "lucide-vue-next"

</script>

<template>
	<div class="drawer">
		<input id="my-drawer" type="checkbox" class="drawer-toggle" />
		<div class="drawer-content min-h-[100dvh]">
			<!-- navbar -->
			<div class="navbar bg-base-100">
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
			</div>
			<!-- navbarend -->

			<slot />

		</div>
		<div class="drawer-side">
			<label for="my-drawer" aria-label="close sidebar" class="drawer-overlay"></label>
			<ul class="menu p-4 w-80 min-h-full bg-base-200 text-base-content">
				<li><a>Sidebar Item 1</a></li>
				<li><a>Sidebar Item 2</a></li>

			</ul>
		</div>
	</div>
</template>