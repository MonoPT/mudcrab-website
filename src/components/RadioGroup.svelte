<script lang="ts">
	import { RadioGroup, useId } from 'bits-ui';

	type RadioItem = {
		label: string;
		value: string;
		description?: string;
		disabled?: boolean;
	};

	let {
		id = useId(),
		label,
		items,
		value = $bindable<string | undefined>(undefined),
		orientation = 'vertical',
		disabled = false,
		required = false
	}: {
		id?: string;
		label: string;
		items: RadioItem[];
		value?: string;
		orientation?: 'horizontal' | 'vertical';
		disabled?: boolean;
		required?: boolean;
	} = $props();
</script>

<div class="field">
	<span class="label">{label}</span>
	<RadioGroup.Root
		{id}
		bind:value
		{orientation}
		{disabled}
		{required}
		class="radio-group {orientation}"
	>
		{#each items as item (item.value)}
			{@const itemId = `${id}-${item.value}`}
			<div class="radio-option">
				<RadioGroup.Item class="radio" id={itemId} value={item.value} disabled={item.disabled}>
					{#snippet children({ checked }: { checked: boolean })}
						{#if checked}<span class="dot" aria-hidden="true"></span>{/if}
					{/snippet}
				</RadioGroup.Item>
				<div class="copy">
					<label for={itemId}>{item.label}</label>
					{#if item.description}<p>{item.description}</p>{/if}
				</div>
			</div>
		{/each}
	</RadioGroup.Root>
</div>

<style>
	.field {
		display: grid;
		gap: 0.65rem;
		min-width: 0;
	}
	.label {
		color: var(--color-text-muted);
		font-size: var(--text-sm);
	}
	:global(.radio-group) {
		display: grid;
		gap: 0.85rem;
	}
	:global(.radio-group.horizontal) {
		grid-template-columns: repeat(3, minmax(0, 1fr));
		gap: 1rem;
	}
	.radio-option {
		display: flex;
		align-items: flex-start;
		gap: 0.7rem;
		min-width: 0;
	}
	:global(.radio) {
		display: inline-flex;
		flex: 0 0 auto;
		align-items: center;
		justify-content: center;
		width: 1.2rem;
		height: 1.2rem;
		margin-top: 0.05rem;
		padding: 0;
		border: 1px solid var(--color-border-strong);
		border-radius: 50%;
		outline: none;
		background: var(--color-surface);
		cursor: pointer;
		transition:
			border-color var(--duration-normal) var(--ease-standard),
			box-shadow var(--duration-normal) var(--ease-standard);
	}
	:global(.radio:hover:not(:disabled)) {
		border-color: var(--color-accent);
	}
	:global(.radio:focus-visible) {
		border-color: var(--color-border-focus);
		box-shadow: var(--focus-ring);
	}
	:global(.radio[data-state='checked']) {
		border-color: var(--color-accent);
	}
	:global(.radio[data-disabled]),
	:global(.radio:disabled) {
		cursor: not-allowed;
		opacity: 0.45;
	}
	.dot {
		width: 0.5rem;
		height: 0.5rem;
		border-radius: 50%;
		background: var(--color-accent);
	}
	.copy {
		display: grid;
		gap: 0.25rem;
		min-width: 0;
	}
	.copy label {
		color: var(--color-text-muted);
		font-size: var(--text-sm);
		line-height: 1.4;
		cursor: pointer;
	}
	.copy p {
		max-width: none;
		font-size: var(--text-xs);
		line-height: 1.45;
	}
	@media (max-width: 700px) {
		:global(.radio-group.horizontal) {
			grid-template-columns: 1fr;
		}
	}
</style>
