<script lang="ts">
	import type { HTMLAttributes } from 'svelte/elements';

	let props: HTMLAttributes<SVGElement> = $props();
</script>

<svg
	class="ssl-icon-remove"
	width="0.875rem"
	height="0.875rem"
	viewBox="0 0 24 24"
	fill="currentColor"
	stroke="currentColor"
	stroke-linecap="round"
	stroke-linejoin="round"
	stroke-width="3"
	pointer-events="none"
	{...props}
>
	<path d="m20.5 3.5-17 17" />
	<path d="m3.5 3.5 17 17" />
</svg>
