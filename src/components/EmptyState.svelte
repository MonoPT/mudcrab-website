<script lang="ts">
	import type { Snippet } from 'svelte';

	let {
		icon,
		title,
		description,
		action
	}: {
		icon?: Snippet;
		title: string;
		description?: string;
		action?: Snippet;
	} = $props();
</script>

<div class="empty-state">
	{#if icon}<div class="empty-icon" aria-hidden="true">{@render icon()}</div>{/if}
	<h3>{title}</h3>
	{#if description}<p>{description}</p>{/if}
	{#if action}<div class="empty-action">{@render action()}</div>{/if}
</div>

<style>
	.empty-state {
		display: grid;
		justify-items: center;
		gap: 0.85rem;
		padding: clamp(2rem, 6vw, 4rem) 1.5rem;
		border: 1px dashed var(--color-border-strong);
		background: var(--color-surface);
		text-align: center;
	}
	.empty-icon {
		display: grid;
		width: 2.75rem;
		height: 2.75rem;
		place-items: center;
		border: 1px solid var(--color-accent-muted);
		border-radius: 50%;
		background: var(--color-info-surface);
		color: var(--color-accent);
	}
	.empty-state h3 {
		font-size: var(--text-lg);
	}
	.empty-state p {
		max-width: 38rem;
		font-size: var(--text-sm);
	}
	.empty-action {
		margin-top: 0.35rem;
	}
</style>
