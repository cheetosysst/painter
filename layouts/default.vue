<script setup lang="ts">
import { Menu } from "lucide-vue-next"

</script>

<template>
	<div class="drawer">
		<input id="my-drawer" type="checkbox" class="drawer-toggle" />
		<div class="drawer-content">
			<!-- navbar -->
			<div class="navbar bg-base-100">
				<div class="flex-none">
					<label for="my-drawer" class="btn btn-square btn-ghost drawer-button">
						<Menu />
					</label>
				</div>
				<div class="flex-1 items-baseline">
					<a href="/" class="inline-grid">

						<span
							class="btn btn-ghost pointer-events-none col-start-1 row-start-1 text-3xl bg-[linear-gradient(90deg,theme(colors.error)_0%,theme(colors.secondary)_9%,theme(colors.secondary)_42%,theme(colors.primary)_47%,theme(colors.accent)_100%)] bg-clip-text blur-xl [transform:translate3d(0,0,0)] [-webkit-text-fill-color:transparent] before:content-[attr(data-text)] [@supports(color:oklch(0_0_0))]:bg-[linear-gradient(90deg,oklch(var(--s))_4%,color-mix(in_oklch,oklch(var(--s)),oklch(var(--er)))_22%,oklch(var(--p))_45%,color-mix(in_oklch,oklch(var(--p)),oklch(var(--a)))_67%,oklch(var(--a))_100.2%)]"
							data-text="PAINTER" aria-hidden="true"></span>
						<span
							class="btn btn-ghost text-3xl [&amp;::selection]:text-base-content relative col-start-1 row-start-1 bg-[linear-gradient(90deg,theme(colors.error)_0%,theme(colors.secondary)_9%,theme(colors.secondary)_42%,theme(colors.primary)_47%,theme(colors.accent)_100%)] bg-clip-text [-webkit-text-fill-color:transparent] [&amp;::selection]:bg-blue-700/20 [@supports(color:oklch(0_0_0))]:bg-[linear-gradient(90deg,oklch(var(--s))_4%,color-mix(in_oklch,oklch(var(--s)),oklch(var(--er)))_22%,oklch(var(--p))_45%,color-mix(in_oklch,oklch(var(--p)),oklch(var(--a)))_67%,oklch(var(--a))_100.2%)]">PAINTER</span>
					</a>
					<span>Placeholder for funny sentences that makes no sense</span>
				</div>
				<div class="flex-none">
					<button class="btn btn-square btn-ghost">
						<Menu />
					</button>
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