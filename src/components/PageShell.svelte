<script lang="ts">
	import type { Snippet } from 'svelte';

	let {
		children,
		width = 'wide',
		class: className = ''
	}: {
		children: Snippet;
		width?: 'narrow' | 'wide' | 'full';
		class?: string;
	} = $props();
</script>

<div class="page-shell {width} {className}">
	{@render children()}
</div>

<style>
	.page-shell {
		width: calc(100% - (var(--page-gutter) * 2));
		margin-inline: auto;
	}
	.page-shell.narrow {
		max-width: var(--content-narrow);
	}
	.page-shell.wide {
		max-width: var(--content-wide);
	}
	.page-shell.full {
		max-width: none;
	}
</style>
