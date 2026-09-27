<script lang="ts">
	import { Menu, X } from '@lucide/svelte';
	import type { Snippet } from 'svelte';

	type NavItem = {
		label: string;
		href: string;
		active?: boolean;
		external?: boolean;
	};

	let {
		brand,
		items = [],
		actions,
		sticky = false,
		mobileLabel = 'Open menu'
	}: {
		brand: Snippet;
		items?: NavItem[];
		actions?: Snippet;
		sticky?: boolean;
		mobileLabel?: string;
	} = $props();

	let menuOpen = $state(false);

	function closeMenu() {
		menuOpen = false;
	}

	function handleKeydown(event: KeyboardEvent) {
		if (event.key === 'Escape') closeMenu();
	}
</script>

<svelte:window onkeydown={handleKeydown} />

<header class="site-header" class:sticky>
	<div class="header-inner">
		{@render brand()}
		<button
			class="menu-toggle"
			type="button"
			aria-label={menuOpen ? 'Close menu' : mobileLabel}
			aria-expanded={menuOpen}
			aria-controls="site-navigation"
			onclick={() => (menuOpen = !menuOpen)}
		>
			{#if menuOpen}
				<X size={20} strokeWidth={1.75} aria-hidden="true" />
			{:else}
				<Menu size={20} strokeWidth={1.75} aria-hidden="true" />
			{/if}
		</button>

		<div class="header-content" class:open={menuOpen}>
			<nav id="site-navigation" aria-label="Main navigation">
				<ul>
					{#each items as item}
						<li>
							<a
								class:active={item.active}
								href={item.href}
								aria-current={item.active ? 'page' : undefined}
								target={item.external ? '_blank' : undefined}
								rel={item.external ? 'noreferrer' : undefined}
								onclick={closeMenu}>{item.label}</a
							>
						</li>
					{/each}
				</ul>
			</nav>
			{#if actions}<div class="header-actions">{@render actions()}</div>{/if}
		</div>
	</div>
</header>

<style>
	.site-header {
		position: relative;
		z-index: var(--z-sticky);
		border-bottom: 1px solid var(--color-border);
		background: color-mix(in srgb, var(--color-background) 92%, transparent);
		backdrop-filter: blur(12px);
	}
	.site-header.sticky {
		position: sticky;
		top: 0;
	}
	.header-inner {
		display: flex;
		align-items: center;
		justify-content: space-between;
		gap: 2rem;
		width: min(100% - 2rem, var(--content-wide));
		min-height: 4.5rem;
		margin: 0 auto;
	}
	.header-content {
		display: flex;
		align-items: center;
		gap: 2rem;
	}
	nav ul {
		display: flex;
		align-items: center;
		gap: 1.5rem;
		margin: 0;
		padding: 0;
		list-style: none;
	}
	nav li + li {
		margin-top: 0;
	}
	nav a {
		position: relative;
		display: inline-flex;
		padding: 0.5rem 0;
		color: var(--color-text-muted);
		font-size: var(--text-xs);
		font-weight: 600;
		letter-spacing: var(--tracking-label);
		text-decoration: none;
		text-transform: uppercase;
	}
	nav a::after {
		position: absolute;
		right: 0;
		bottom: 0;
		left: 0;
		height: 1px;
		background: var(--color-accent);
		content: '';
		transform: scaleX(0);
		transform-origin: right;
		transition: transform var(--duration-normal) var(--ease-standard);
	}
	nav a:hover,
	nav a.active {
		color: var(--color-text);
	}
	nav a:hover::after,
	nav a.active::after {
		transform: scaleX(1);
		transform-origin: left;
	}
	nav a:focus-visible,
	.menu-toggle:focus-visible {
		outline: none;
		box-shadow: var(--focus-ring);
	}
	.header-actions {
		display: flex;
		align-items: center;
		gap: 0.6rem;
	}
	.menu-toggle {
		display: none;
		place-items: center;
		width: 2.5rem;
		height: 2.5rem;
		padding: 0;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-sm);
		background: transparent;
		color: var(--color-text-muted);
		cursor: pointer;
	}
	@media (max-width: 700px) {
		.header-inner {
			position: relative;
			min-height: 4rem;
		}
		.menu-toggle {
			display: grid;
		}
		.header-content {
			position: absolute;
			top: calc(100% + 1px);
			right: 0;
			left: 0;
			display: none;
			align-items: stretch;
			gap: 1rem;
			padding: 1rem;
			border: 1px solid var(--color-border);
			border-top: 0;
			background: var(--color-surface-raised);
			box-shadow: var(--shadow-md);
		}
		.header-content.open {
			display: grid;
		}
		nav ul {
			display: grid;
			gap: 0.25rem;
		}
		nav a {
			width: 100%;
			padding: 0.7rem 0.5rem;
		}
		.header-actions {
			padding-top: 1rem;
			border-top: 1px solid var(--color-border);
		}
	}
	@media (prefers-reduced-motion: reduce) {
		nav a::after {
			transition: none;
		}
	}
</style>
