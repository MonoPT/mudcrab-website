<script lang="ts">
	let {
		ornament = false,
		label,
		spacing = 'md'
	}: {
		ornament?: boolean;
		label?: string;
		spacing?: 'sm' | 'md' | 'lg';
	} = $props();
</script>

<div class="divider {spacing}" class:ornament role="separator" aria-label={label}>
	{#if ornament}<span aria-hidden="true">ᛉ</span>{/if}
</div>

<style>
	.divider {
		display: flex;
		height: 1px;
		align-items: center;
		width: 100%;
		background: linear-gradient(90deg, var(--color-border), transparent);
	}
	.divider.sm {
		margin-block: var(--space-4);
	}
	.divider.md {
		margin-block: var(--space-8);
	}
	.divider.lg {
		margin-block: var(--space-16);
	}
	.divider.ornament {
		justify-content: center;
		background: linear-gradient(
			90deg,
			transparent,
			var(--color-border) 30%,
			var(--color-border) 70%,
			transparent
		);
	}
	.divider.ornament span {
		display: grid;
		width: 2rem;
		height: 2rem;
		place-items: center;
		border: 1px solid var(--color-border-strong);
		background: var(--color-background);
		color: var(--color-accent);
		font: 0.9rem var(--font-display);
		transform: rotate(45deg);
	}
	.divider.ornament span::first-letter {
		transform: rotate(-45deg);
	}
</style>
