<script lang="ts">
	import type { Snippet } from 'svelte';

	type Tone = 'neutral' | 'accent' | 'success' | 'warning' | 'danger';
	type Size = 'sm' | 'md';

	let {
		tone = 'neutral',
		size = 'sm',
		children,
		icon
	}: {
		tone?: Tone;
		size?: Size;
		children: Snippet;
		icon?: Snippet;
	} = $props();
</script>

<span class="badge {tone} {size}">
	{#if icon}<span class="icon" aria-hidden="true">{@render icon()}</span>{/if}
	<span>{@render children()}</span>
</span>

<style>
	.badge {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: 0.4rem;
		width: fit-content;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-pill);
		color: var(--color-text-muted);
		font-size: var(--text-xs);
		font-weight: 600;
		letter-spacing: 0.12em;
		line-height: 1;
		text-transform: uppercase;
		white-space: nowrap;
	}

	.sm { min-height: 1.5rem; padding: 0.35rem 0.6rem; }
	.md { min-height: 1.9rem; padding: 0.45rem 0.8rem; font-size: var(--text-sm); }

	.neutral { border-color: var(--color-border-strong); color: var(--color-text-muted); }
	.accent { border-color: color-mix(in srgb, var(--color-accent), transparent 45%); color: var(--color-accent); background: color-mix(in srgb, var(--color-accent), transparent 92%); }
	.success { border-color: color-mix(in srgb, var(--color-success), transparent 45%); color: var(--color-success); background: color-mix(in srgb, var(--color-success), transparent 92%); }
	.warning { border-color: color-mix(in srgb, var(--color-warning), transparent 45%); color: var(--color-warning); background: color-mix(in srgb, var(--color-warning), transparent 92%); }
	.danger { border-color: color-mix(in srgb, var(--color-danger), transparent 45%); color: var(--color-danger); background: color-mix(in srgb, var(--color-danger), transparent 92%); }

	.icon { display: inline-flex; align-items: center; }
	.icon :global(svg) { width: 0.8rem; height: 0.8rem; }
	.md .icon :global(svg) { width: 0.95rem; height: 0.95rem; }
</style>
