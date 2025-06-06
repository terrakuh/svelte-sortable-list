<script lang="ts">
	import { onMount } from 'svelte';
	import {
		SortableList,
		SortableItem,
		removeItem,
		sortItems,
		type RemoveEventDetail,
		type SortEventDetail,
	} from '$lib/index.js';
	import { defaultItems, defaultProps } from '../fixtures.js';
	import { rootProps } from '../stores.js';
	import '$lib/styles.css';

	let dialogRef: HTMLDialogElement;

	let items = $state([...defaultItems]);

	onMount(() => {
		$rootProps = { ...defaultProps };
	});

	function handleSort({ prevItemIndex, nextItemIndex }: SortEventDetail) {
		items = sortItems(items, prevItemIndex, nextItemIndex);
	}

	function handleRemove({ itemIndex }: RemoveEventDetail) {
		items = removeItem(items, itemIndex);
	}

	function handleClickDialog(event: MouseEvent) {
		const target = event.target as HTMLElement;
		if (target?.nodeName === 'DIALOG') handleCloseDialog();
	}

	function handleOpenDialog() {
		dialogRef.showModal();
	}

	function handleCloseDialog() {
		dialogRef.close();
	}
</script>

<svelte:head>
	<title>Inside dialog | Svelte Sortable List</title>
</svelte:head>

<button class="button" onclick={handleOpenDialog}>Open dialog</button>
<dialog bind:this={dialogRef} class="dialog" onclick={handleClickDialog}>
	<div class="dialog__inner">
		<button class="dialog__close button" onclick={handleCloseDialog}>Close dialog</button>
		<SortableList {...$rootProps} onSort={handleSort} onRemove={handleRemove}>
			{#each items as item, index (item.id)}
				<SortableItem {...item} {index}>
					<div class="ssl-item__content">
						{item.text}
					</div>
				</SortableItem>
			{/each}
		</SortableList>
	</div>
</dialog>

<style lang="scss">
	:global(html:has(dialog[open])) {
		overflow: hidden;
	}

	.dialog {
		width: 40rem;
		max-width: 90vw;
		max-width: 90dvw;
		padding: 0;
		background-color: var(--gray-100);
		box-shadow: var(--box-shadow-4);
		border: none;
		color: inherit;
		z-index: 1;

		&:not([open]) {
			pointer-events: none;
			opacity: 0;
		}

		&[open] {
			pointer-events: auto;
			opacity: 1;
			animation: fade-in 320ms forwards;
		}

		&__inner {
			padding: 4rem;
		}

		&__close {
			position: absolute;
			top: 1rem;
			right: 1rem;
			height: 2.25rem;
			font-size: 0.875rem;
		}

		&::backdrop {
			background-color: rgba(0, 0, 0, 0.32);
		}
	}

	@keyframes fade-in {
		0% {
			opacity: 0;
		}
		100% {
			opacity: 1;
		}
	}

	@keyframes fade-out {
		0% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}
</style>
