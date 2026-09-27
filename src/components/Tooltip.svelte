<script lang="ts">
	import { Tooltip as TooltipPrimitive } from 'bits-ui';
	import type { Snippet } from 'svelte';

	let {
		content,
		side = 'top',
		delay = 300,
		children
	}: {
		content: string;
		side?: 'top' | 'right' | 'bottom' | 'left';
		delay?: number;
		children: Snippet;
	} = $props();
</script>

<TooltipPrimitive.Provider delayDuration={delay}>
	<TooltipPrimitive.Root>
		<TooltipPrimitive.Trigger class="tooltip-trigger">
			{@render children()}
		</TooltipPrimitive.Trigger>
		<TooltipPrimitive.Portal>
			<TooltipPrimitive.Content class="tooltip-content" {side} sideOffset={8}>
				{content}
				<TooltipPrimitive.Arrow class="tooltip-arrow" />
			</TooltipPrimitive.Content>
		</TooltipPrimitive.Portal>
	</TooltipPrimitive.Root>
</TooltipPrimitive.Provider>

<style>
	:global(.tooltip-trigger) {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		min-height: 2.5rem;
		padding: 0.6rem 0.9rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-sm);
		outline: none;
		background: var(--color-surface);
		color: var(--color-text-muted);
		font: 600 var(--text-xs) var(--font-body);
		cursor: help;
		transition:
			border-color var(--duration-normal) var(--ease-standard),
			color var(--duration-normal) var(--ease-standard),
			box-shadow var(--duration-normal) var(--ease-standard);
	}
	:global(.tooltip-trigger:hover) {
		border-color: var(--color-accent);
		color: var(--color-text);
	}
	:global(.tooltip-trigger:focus-visible) {
		border-color: var(--color-border-focus);
		box-shadow: var(--focus-ring);
		color: var(--color-accent);
	}
	:global(.tooltip-content) {
		z-index: var(--z-tooltip);
		max-width: 16rem;
		padding: 0.55rem 0.7rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-sm);
		background: var(--color-surface-raised);
		box-shadow: var(--shadow-md);
		color: var(--color-text-muted);
		font-size: var(--text-xs);
		line-height: 1.45;
	}
	:global(.tooltip-arrow) {
		fill: var(--color-surface-raised);
		stroke: var(--color-border-strong);
	}
</style>
