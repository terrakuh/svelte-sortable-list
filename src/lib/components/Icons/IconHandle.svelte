<script lang="ts">
	import type { HTMLAttributes } from 'svelte/elements';

	let props: HTMLAttributes<SVGElement> = $props();
</script>

<svg
	class="ssl-icon-handle"
	fill="currentColor"
	height="0.875rem"
	viewBox="0 0 320 512"
	pointer-events="none"
	{...props}
>
	<circle cx="80" cy="96" r="48" />
	<circle cx="240" cy="96" r="48" />
	<circle cx="80" cy="256" r="48" />
	<circle cx="240" cy="256" r="48" />
	<circle cx="80" cy="416" r="48" />
	<circle cx="240" cy="416" r="48" />
</svg>
