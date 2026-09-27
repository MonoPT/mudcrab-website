<script lang="ts">
	import { Tabs } from 'bits-ui';

	type TabItem = {
		value: string;
		label: string;
		content: string;
		disabled?: boolean;
	};

	let {
		items,
		value = $bindable<string | undefined>(undefined),
		orientation = 'horizontal',
		activation = 'automatic',
		disabled = false
	}: {
		items: TabItem[];
		value?: string;
		orientation?: 'horizontal' | 'vertical';
		activation?: 'automatic' | 'manual';
		disabled?: boolean;
	} = $props();
</script>

<Tabs.Root
	bind:value
	{orientation}
	activationMode={activation}
	{disabled}
	class="tabs {orientation}"
>
	<Tabs.List class="tabs-list">
		{#each items as item (item.value)}
			<Tabs.Trigger class="tabs-trigger" value={item.value} disabled={item.disabled}>
				{item.label}
			</Tabs.Trigger>
		{/each}
	</Tabs.List>

	{#each items as item (item.value)}
		<Tabs.Content class="tabs-content" value={item.value}>{item.content}</Tabs.Content>
	{/each}
</Tabs.Root>

<style>
	:global(.tabs) {
		display: grid;
		gap: 1.25rem;
	}
	:global(.tabs.vertical) {
		grid-template-columns: minmax(8rem, 0.35fr) minmax(0, 1fr);
		align-items: start;
		gap: 1.5rem;
	}
	:global(.tabs-list) {
		display: flex;
		gap: 0.25rem;
		border-bottom: 1px solid var(--color-border);
		overflow-x: auto;
	}
	:global(.tabs.vertical .tabs-list) {
		display: grid;
		border-right: 1px solid var(--color-border);
		border-bottom: 0;
		overflow-x: visible;
	}
	:global(.tabs-trigger) {
		position: relative;
		flex: 0 0 auto;
		padding: 0.75rem 0.9rem;
		border: 0;
		outline: none;
		background: transparent;
		color: var(--color-text-subtle);
		font: 600 var(--text-xs) var(--font-body);
		letter-spacing: var(--tracking-label);
		text-transform: uppercase;
		white-space: nowrap;
		cursor: pointer;
		transition: color var(--duration-normal) var(--ease-standard);
	}
	:global(.tabs-trigger::after) {
		position: absolute;
		right: 0.9rem;
		bottom: -1px;
		left: 0.9rem;
		height: 2px;
		background: transparent;
		content: '';
		transition: background var(--duration-normal) var(--ease-standard);
	}
	:global(.tabs-trigger:hover:not(:disabled)),
	:global(.tabs-trigger[data-state='active']) {
		color: var(--color-text);
	}
	:global(.tabs-trigger[data-state='active']::after) {
		background: var(--color-accent);
	}
	:global(.tabs-trigger:focus-visible) {
		color: var(--color-accent);
		box-shadow: var(--focus-ring);
	}
	:global(.tabs-trigger:disabled) {
		cursor: not-allowed;
		opacity: 0.45;
	}
	:global(.tabs.vertical .tabs-trigger) {
		text-align: left;
	}
	:global(.tabs.vertical .tabs-trigger::after) {
		top: 0;
		right: -1px;
		bottom: 0;
		left: auto;
		width: 2px;
		height: auto;
	}
	:global(.tabs-content) {
		max-width: 42rem;
		color: var(--color-text-muted);
		font-size: var(--text-sm);
		line-height: 1.6;
	}
	@media (max-width: 560px) {
		:global(.tabs.vertical) {
			grid-template-columns: 1fr;
		}
		:global(.tabs.vertical .tabs-list) {
			display: flex;
			border-right: 0;
			border-bottom: 1px solid var(--color-border);
			overflow-x: auto;
		}
	}
</style>
