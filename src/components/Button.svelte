<script lang="ts">
	import type { Snippet } from 'svelte';

	type Variant = 'primary' | 'secondary' | 'ghost' | 'danger' | 'button';
	type Size = 'sm' | 'md' | 'lg';

	let {
		variant = 'secondary',
		size = 'md',
		type = 'button',
		disabled = false,
		loading = false,
		label,
		children,
		leading,
		trailing
	}: {
		variant?: Variant;
		size?: Size;
		type?: 'button' | 'submit' | 'reset';
		disabled?: boolean;
		loading?: boolean;
		label?: string;
		children?: Snippet;
		leading?: Snippet;
		trailing?: Snippet;
	} = $props();
</script>

<button
	class="button {variant} {size}"
	class:icon-only={variant === 'button'}
	{type}
	disabled={disabled || loading}
	aria-label={variant === 'button' ? label : undefined}
	aria-busy={loading}
>
	{#if loading}
		<span class="spinner" aria-hidden="true"></span>
	{:else if leading}
		<span class="icon" aria-hidden="true">{@render leading()}</span>
	{/if}
	{#if children}{@render children()}{/if}
	{#if !loading && trailing}
		<span class="icon" aria-hidden="true">{@render trailing()}</span>
	{/if}
</button>

<style>
	.button {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		gap: 0.6rem;
		min-height: 2.5rem;
		padding: 0.65rem 1rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-sm);
		background: transparent;
		color: var(--color-text);
		font-size: var(--text-xs);
		font-weight: 600;
		letter-spacing: 0.1em;
		line-height: 1;
		text-transform: uppercase;
		cursor: pointer;
		transition:
			background var(--duration-normal) var(--ease-standard),
			border-color var(--duration-normal) var(--ease-standard),
			color var(--duration-normal) var(--ease-standard),
			transform var(--duration-normal) var(--ease-standard);
	}

	.button:hover:not(:disabled) {
		border-color: var(--color-accent);
		background: var(--color-surface-hover);
		transform: translateY(-1px);
	}

	.button:active:not(:disabled) {
		transform: translateY(0);
	}

	.primary {
		border-color: var(--color-accent);
		background: var(--color-accent);
		color: var(--color-accent-ink);
	}

	.primary:hover:not(:disabled) {
		border-color: var(--color-accent-hover);
		background: var(--color-accent-hover);
	}

	.ghost {
		border-color: transparent;
		color: var(--color-accent);
	}

	.ghost:hover:not(:disabled) {
		border-color: var(--color-border);
	}

	.danger {
		border-color: color-mix(in srgb, var(--color-danger), transparent 40%);
		color: var(--color-danger);
	}

	.danger:hover:not(:disabled) {
		background: var(--color-danger-surface);
	}

	.icon-only {
		width: 2.5rem;
		min-width: 2.5rem;
		padding: 0;
		border-radius: var(--radius-md);
	}

	.sm { min-height: 2rem; padding: 0.5rem 0.75rem; }
	.lg { min-height: 3rem; padding: 0.8rem 1.25rem; }
	.icon-only.sm { width: 2rem; min-width: 2rem; }
	.icon-only.lg { width: 3rem; min-width: 3rem; }

	.icon,
	.spinner { display: inline-flex; flex: 0 0 auto; align-items: center; justify-content: center; }
	.icon :global(svg) { width: 1rem; height: 1rem; }
	.icon-only :global(svg) { width: 1.1rem; height: 1.1rem; }
	.icon-only.sm :global(svg) { width: 1.05rem; height: 1.05rem; }
	.icon-only.lg :global(svg) { width: 1.2rem; height: 1.2rem; }
	.spinner { width: 0.9rem; height: 0.9rem; border: 2px solid currentColor; border-right-color: transparent; border-radius: 50%; animation: spin 0.7s linear infinite; }

	:disabled { opacity: 0.45; cursor: not-allowed; }

	@keyframes spin { to { transform: rotate(360deg); } }
	@media (prefers-reduced-motion: reduce) { .spinner { animation: none; border-right-color: currentColor; opacity: 0.7; } }
</style>
