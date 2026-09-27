<script lang="ts">
	import type { Snippet } from 'svelte';

	type Variant = 'default' | 'feature' | 'media' | 'interactive';

	let {
		variant = 'default',
		href,
		eyebrow,
		title,
		description,
		image,
		imageAlt,
		children,
		footer
	}: {
		variant?: Variant;
		href?: string;
		eyebrow?: string;
		title?: string;
		description?: string;
		image?: string;
		imageAlt?: string;
		children?: Snippet;
		footer?: Snippet;
	} = $props();
</script>

<article class="card {variant}" class:has-image={image}>
	{#if href}
		<a class="card-link" {href} aria-label={title}>
			<div class="card-content">
				{#if image}<img src={image} alt={imageAlt ?? title ?? ''} loading="lazy" />{/if}
				{#if variant === 'media' && children}<div class="media-content">
						{@render children()}
					</div>{/if}
				<div class="card-body">
					{#if eyebrow}<p class="eyebrow">{eyebrow}</p>{/if}
					{#if title}<h3>{title}</h3>{/if}
					{#if description}<p>{description}</p>{/if}
					{#if children && variant !== 'media'}<div class="slot-content">
							{@render children()}
						</div>{/if}
				</div>
			</div>
		</a>
	{:else}
		<div class="card-content">
			{#if image}<img src={image} alt={imageAlt ?? title ?? ''} loading="lazy" />{/if}
			{#if variant === 'media' && children}<div class="media-content">
					{@render children()}
				</div>{/if}
			<div class="card-body">
				{#if eyebrow}<p class="eyebrow">{eyebrow}</p>{/if}
				{#if title}<h3>{title}</h3>{/if}
				{#if description}<p>{description}</p>{/if}
				{#if children && variant !== 'media'}<div class="slot-content">
						{@render children()}
					</div>{/if}
			</div>
		</div>
	{/if}
	{#if footer}<div class="card-footer">{@render footer()}</div>{/if}
</article>

<style>
	.card {
		position: relative;
		overflow: hidden;
		border: 1px solid var(--color-border);
		border-radius: var(--radius-md);
		background: linear-gradient(145deg, rgb(19 31 38 / 0.95), rgb(10 17 21 / 0.95));
		box-shadow: var(--shadow-sm);
	}

	.card-content {
		height: 100%;
	}
	.card-body {
		padding: 1.35rem;
	}
	.card h3 {
		margin: 0.45rem 0 0.7rem;
		font-size: var(--text-xl);
	}
	.card p:not(.eyebrow) {
		font-size: var(--text-sm);
	}
	.card .eyebrow {
		margin: 0;
	}
	.card img {
		display: block;
		width: 100%;
		aspect-ratio: 16 / 9;
		object-fit: cover;
		border-bottom: 1px solid var(--color-border);
	}
	.media-content {
		border-bottom: 1px solid var(--color-border);
	}
	.media-content :global(img),
	.media-content :global(video) {
		display: block;
		width: 100%;
	}
	.card-footer {
		display: flex;
		align-items: center;
		gap: 0.75rem;
		padding: 0 1.35rem 1.35rem;
	}
	.slot-content {
		margin-top: 1rem;
	}

	.feature {
		background: linear-gradient(145deg, rgb(28 47 59 / 0.9), rgb(10 17 21 / 0.95));
	}
	.feature h3 {
		font-size: var(--text-2xl);
	}
	.media .card-body {
		padding-top: 1rem;
	}
	.interactive {
		transition:
			border-color var(--duration-normal) var(--ease-standard),
			transform var(--duration-normal) var(--ease-standard),
			box-shadow var(--duration-normal) var(--ease-standard);
	}
	.interactive:hover {
		border-color: var(--color-accent-muted);
		box-shadow: var(--shadow-md);
		transform: translateY(-2px);
	}

	.card-link {
		display: block;
		height: 100%;
		color: inherit;
		text-decoration: none;
	}
	.card-link:focus-visible {
		outline-offset: -4px;
	}
	.card-link:hover h3 {
		color: var(--color-accent);
	}
	.card-link h3 {
		transition: color var(--duration-normal) var(--ease-standard);
	}

	@media (prefers-reduced-motion: reduce) {
		.interactive,
		.card-link h3 {
			transition: none;
		}
	}
</style>
