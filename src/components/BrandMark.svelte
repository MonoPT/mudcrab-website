<script lang="ts">
	let {
		name = 'Mudcrab',
		subtitle,
		compact = false,
		href = '/',
		class: className = ''
	}: {
		name?: string;
		subtitle?: string;
		compact?: boolean;
		href?: string;
		class?: string;
	} = $props();
</script>

<a class="brand-mark {className}" class:compact {href} aria-label={compact ? name : undefined}>
	<span class="brand-symbol" aria-hidden="true">ᛉ</span>
	{#if !compact}
		<span class="brand-copy">
			<strong>{name}</strong>
			{#if subtitle}<span>{subtitle}</span>{/if}
		</span>
	{/if}
</a>

<style>
	.brand-mark {
		display: inline-flex;
		align-items: center;
		gap: 0.8rem;
		width: fit-content;
		color: var(--color-text);
		text-decoration: none;
	}
	.brand-mark:hover .brand-symbol {
		border-color: var(--color-accent);
		color: var(--color-accent-hover);
	}
	.brand-mark:focus-visible {
		outline: none;
		box-shadow: var(--focus-ring);
	}
	.brand-symbol {
		display: grid;
		width: 2.25rem;
		height: 2.25rem;
		flex: 0 0 auto;
		place-items: center;
		border: 1px solid var(--color-border-strong);
		color: var(--color-accent);
		font: 1.25rem var(--font-display);
		transform: rotate(45deg);
		transition:
			border-color var(--duration-normal) var(--ease-standard),
			color var(--duration-normal) var(--ease-standard);
	}
	.brand-symbol::first-letter {
		display: block;
		transform: rotate(-45deg);
	}
	.brand-copy {
		display: grid;
		gap: 0.15rem;
	}
	.brand-copy strong {
		font: 600 var(--text-md) var(--font-display);
		letter-spacing: var(--tracking-display);
	}
	.brand-copy span {
		color: var(--color-text-subtle);
		font-size: var(--text-xs);
		letter-spacing: var(--tracking-label);
		text-transform: uppercase;
	}
	.brand-mark.compact .brand-symbol {
		width: 2.5rem;
		height: 2.5rem;
	}
</style>
