<script lang="ts">
	import { ChevronDown } from '@lucide/svelte';
	import { Select } from 'bits-ui';

	type SelectItem = {
		label: string;
		value: string;
		disabled?: boolean;
	};

	let {
		id = 'select-input',
		label,
		items,
		value = $bindable<string | undefined>(undefined),
		placeholder = 'Select an option',
		disabled = false,
		error
	}: {
		id?: string;
		label: string;
		items: SelectItem[];
		value?: string;
		placeholder?: string;
		disabled?: boolean;
		error?: string;
	} = $props();

	let errorId = $derived(error ? `${id}-error` : undefined);
</script>

<div class="field" class:error-state={error}>
	<label for={id}>{label}</label>
	<Select.Root type="single" {items} {disabled} bind:value>
		<Select.Trigger
			class="trigger"
			{id}
			{disabled}
			aria-invalid={error ? 'true' : undefined}
			aria-describedby={errorId}
		>
			<Select.Value {placeholder} />
			<ChevronDown class="chevron" size={16} strokeWidth={1.75} aria-hidden="true" />
		</Select.Trigger>
		<Select.Portal>
			<Select.Content class="content" sideOffset={6}>
				<Select.Viewport>
					{#each items as item (item.value)}
						<Select.Item
							class="item"
							value={item.value}
							label={item.label}
							disabled={item.disabled}
						>
							{#snippet children({ selected }: { selected: boolean })}
								<span>{item.label}</span>
								{#if selected}<span class="indicator" aria-hidden="true">✓</span>{/if}
							{/snippet}
						</Select.Item>
					{/each}
				</Select.Viewport>
			</Select.Content>
		</Select.Portal>
	</Select.Root>
	{#if error}<p class="error" id={errorId}>{error}</p>{/if}
</div>

<style>
	.field {
		position: relative;
		display: grid;
		align-content: start;
		gap: 0.45rem;
		min-width: 0;
	}
	label {
		color: var(--color-text-muted);
		font-size: var(--text-sm);
	}
	:global(.trigger) {
		display: flex;
		align-items: center;
		justify-content: space-between;
		width: 100%;
		height: 2.65rem;
		padding: 0.65rem 0.8rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-sm);
		outline: none;
		background: var(--color-surface);
		color: var(--color-text);
		font-size: var(--text-sm);
		text-align: left;
		cursor: pointer;
		transition:
			border-color var(--duration-normal) var(--ease-standard),
			box-shadow var(--duration-normal) var(--ease-standard);
	}
	:global(.trigger:hover:not(:disabled)) {
		border-color: var(--color-accent-muted);
	}
	:global(.trigger:focus-visible) {
		border-color: var(--color-border-focus);
		box-shadow: var(--focus-ring);
	}
	:global(.trigger[data-placeholder]) {
		color: var(--color-text-subtle);
	}
	:global(.trigger:disabled) {
		cursor: not-allowed;
		opacity: 0.5;
	}
	:global(.chevron) {
		display: block;
		flex: 0 0 auto;
		color: var(--color-text-subtle);
	}
	:global(.content) {
		z-index: var(--z-dropdown);
		width: var(--bits-select-anchor-width);
		min-width: var(--bits-select-anchor-width);
		max-height: 18rem;
		overflow: hidden;
		padding: 0.35rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-md);
		background: var(--color-surface-raised);
		box-shadow: var(--shadow-md);
	}
	:global([data-select-viewport]) {
		max-height: 17rem;
		overflow: auto;
	}
	:global(.item) {
		position: relative;
		display: flex;
		align-items: center;
		justify-content: space-between;
		min-height: 2.3rem;
		padding: 0.55rem 0.65rem;
		border-radius: var(--radius-sm);
		outline: none;
		color: var(--color-text-muted);
		font-size: var(--text-sm);
		cursor: pointer;
	}
	:global(.item:hover),
	:global(.item[data-highlighted]) {
		background: var(--color-surface-hover);
		color: var(--color-text);
	}
	:global(.item[data-disabled]) {
		cursor: not-allowed;
		opacity: 0.45;
	}
	:global(.indicator) {
		color: var(--color-accent);
	}
	.field p {
		max-width: none;
		font-size: var(--text-xs);
		line-height: 1.45;
	}
	.error {
		color: var(--color-danger);
	}
	.error-state :global(.trigger) {
		border-color: color-mix(in srgb, var(--color-danger), transparent 35%);
	}
</style>
