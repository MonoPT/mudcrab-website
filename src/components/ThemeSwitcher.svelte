<script lang="ts">
	import { Palette } from '@lucide/svelte';
	import { onMount } from 'svelte';

	const storageKey = 'mudcrab-theme';
	const themeLoaders = import.meta.glob('../themes/*.css', {
		query: '?inline',
		import: 'default'
	}) as Record<string, () => Promise<string>>;

	const themes = [
		{ value: 'default', label: 'Mudcrab' },
		...Object.keys(themeLoaders).map((path) => {
			const value =
				path
					.split('/')
					.pop()
					?.replace(/\.css$/, '') ?? path;
			return {
				value,
				label: value.replace(/[-_]+/g, ' ').replace(/\b\w/g, (character) => character.toUpperCase())
			};
		})
	];

	let selectedTheme = $state('default');
	let open = $state(false);
	let switcher: HTMLDivElement;
	let themeStyle: HTMLStyleElement | undefined;
	let loadVersion = 0;

	function selectTheme(theme: string) {
		selectedTheme = theme;
		localStorage.setItem(storageKey, selectedTheme);
		open = false;
	}

	function handleWindowClick(event: MouseEvent) {
		if (event.target instanceof Node && !switcher?.contains(event.target)) open = false;
	}

	function handleKeydown(event: KeyboardEvent) {
		if (event.key === 'Escape') open = false;
	}

	onMount(() => {
		const savedTheme = localStorage.getItem(storageKey);
		if (savedTheme && themes.some((theme) => theme.value === savedTheme)) {
			selectedTheme = savedTheme;
		}

		return () => themeStyle?.remove();
	});

	$effect(() => {
		const version = ++loadVersion;
		themeStyle?.remove();
		themeStyle = undefined;

		if (selectedTheme === 'default') return;

		const loader = themeLoaders[`../themes/${selectedTheme}.css`];
		if (!loader) return;

		void loader().then((css) => {
			if (version !== loadVersion) return;

			themeStyle = document.createElement('style');
			themeStyle.dataset.theme = selectedTheme;
			themeStyle.textContent = css;
			document.head.append(themeStyle);
		});
	});
</script>

<svelte:window onclick={handleWindowClick} onkeydown={handleKeydown} />

<div class="theme-switcher" bind:this={switcher}>
	<button
		class="theme-trigger"
		type="button"
		aria-label="Choose theme"
		aria-expanded={open}
		aria-haspopup="listbox"
		onclick={() => (open = !open)}
	>
		<Palette size={17} strokeWidth={1.75} aria-hidden="true" />
	</button>

	{#if open}
		<div class="theme-menu" role="listbox" aria-label="Theme">
			{#each themes as theme (theme.value)}
				<button
					type="button"
					role="option"
					aria-selected={selectedTheme === theme.value}
					class:selected={selectedTheme === theme.value}
					onclick={() => selectTheme(theme.value)}
				>
					{theme.label}
				</button>
			{/each}
		</div>
	{/if}
</div>

<style>
	.theme-switcher {
		position: relative;
		display: inline-flex;
		color: var(--color-text-subtle);
	}
	.theme-trigger {
		display: grid;
		width: 2.35rem;
		height: 2.35rem;
		place-items: center;
		padding: 0;
		border: 1px solid transparent;
		border-radius: var(--radius-sm);
		outline: none;
		background: transparent;
		color: var(--color-accent);
		cursor: pointer;
		transition:
			background var(--duration-normal) var(--ease-standard),
			border-color var(--duration-normal) var(--ease-standard),
			transform var(--duration-normal) var(--ease-standard);
	}
	.theme-trigger:hover,
	.theme-trigger[aria-expanded='true'] {
		border-color: var(--color-border);
		background: var(--color-surface-hover);
		transform: translateY(-1px);
	}
	.theme-trigger:active {
		transform: translateY(0);
	}
	.theme-trigger:focus-visible,
	.theme-menu button:focus-visible {
		box-shadow: var(--focus-ring);
	}
	.theme-menu {
		position: absolute;
		top: calc(100% + 0.5rem);
		right: 0;
		z-index: var(--z-dropdown);
		display: grid;
		min-width: 10rem;
		padding: 0.35rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-md);
		background: var(--color-surface-raised);
		box-shadow: var(--shadow-md);
	}
	.theme-menu button {
		padding: 0.6rem 0.7rem;
		border: 0;
		border-radius: var(--radius-sm);
		outline: none;
		background: transparent;
		color: var(--color-text-muted);
		font: 600 var(--text-xs) var(--font-body);
		letter-spacing: 0.08em;
		text-align: left;
		text-transform: uppercase;
		cursor: pointer;
	}
	.theme-menu button:hover,
	.theme-menu button.selected {
		background: var(--color-surface-hover);
		color: var(--color-text);
	}
</style>
