<script lang="ts">
	import { createCollapsible } from '$lib/builders/collapsible';
	import { PreviewWrapper } from '$docs/components';
	import { slide } from 'svelte/transition';
	import X from '~icons/lucide/x';
	import ChevronsUpDown from '~icons/lucide/chevrons-up-down';

	let openProp: boolean;
	let disabledProp: boolean;
	export { openProp as open, disabledProp as disabled };

	const { open, root, content, trigger, disabled } = createCollapsible({
		open: openProp,
		disabled: disabledProp,
	});

	$: $open = openProp;
	$: $disabled = disabledProp;
</script>

<PreviewWrapper>
	<div melt={$root} class="mx-auto w-screen max-w-md">
		<div class="flex items-center justify-between">
			<span class="text-sm leading-6 text-white"> @thomasglopes starred 3 repositories </span>
			<button
				melt={$trigger}
				class="relative h-6 w-6 place-items-center rounded-full bg-white text-sm text-magnum-700
				shadow-lg hover:opacity-75
				data-[disabled]:cursor-not-allowed data-[disabled]:opacity-75"
			>
				<div class="abs-center">
					{#if $open}
						<X />
					{:else}
						<ChevronsUpDown />
					{/if}
				</div>
			</button>
		</div>

		<div class="my-2 rounded bg-white p-3 shadow-lg">
			<span class="text-base leading-6 text-magnum-800">melt-ui/melt-ui</span>
		</div>

		{#if $open}
			<div melt={$content} transition:slide>
				<div class="flex flex-col gap-2">
					<div class="rounded bg-white p-3 shadow-lg">
						<span class="text-base leading-6 text-magnum-800">sveltejs/svelte</span>
					</div>
					<div class="rounded bg-white p-3 shadow-lg">
						<span class="text-base leading-6 text-magnum-800">sveltejs/kit</span>
					</div>
				</div>
			</div>
		{/if}
	</div>
</PreviewWrapper>

<style>
	.abs-center {
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
	}
</style>
