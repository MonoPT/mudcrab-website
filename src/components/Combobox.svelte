<script lang="ts">
	import { Check, ChevronDown, Search } from '@lucide/svelte';
	import { Combobox } from 'bits-ui';

	type ComboboxItem = {
		label: string;
		value: string;
		disabled?: boolean;
	};

	let {
		id = 'combobox-input',
		label,
		items,
		value = $bindable<string | string[] | undefined>(undefined),
		multiple = false,
		placeholder = 'Search options...',
		description,
		error,
		disabled = false,
		required = false
	}: {
		id?: string;
		label: string;
		items: ComboboxItem[];
		value?: string | string[];
		multiple?: boolean;
		placeholder?: string;
		description?: string;
		error?: string;
		disabled?: boolean;
		required?: boolean;
	} = $props();

	let searchValue = $state('');
	let open = $state(false);
	let descriptionId = $derived(description ? `${id}-description` : undefined);
	let errorId = $derived(error ? `${id}-error` : undefined);
	let describedBy = $derived([descriptionId, errorId].filter(Boolean).join(' ') || undefined);
	let filteredItems = $derived(
		searchValue === ''
			? items
			: items.filter((item) => item.label.toLowerCase().includes(searchValue.toLowerCase()))
	);
	let selectedLabels = $derived(
		Array.isArray(value)
			? value
					.map((selectedValue) => items.find((item) => item.value === selectedValue)?.label)
					.filter((item): item is string => Boolean(item))
					.join(', ')
			: ''
	);

	function handleInput(event: Event & { currentTarget: HTMLInputElement }) {
		searchValue = event.currentTarget.value;
	}

	function handleOpenChange(isOpen: boolean) {
		if (!isOpen) searchValue = '';
	}

	function handleValueChange() {
		if (!multiple) {
			open = false;
			searchValue = '';
		}
	}
</script>

<div
	class="field"
	class:error-state={error}
	class:has-selection={multiple && Boolean(selectedLabels)}
>
	<label for={id}
		>{label}{#if required}<span class="required" aria-hidden="true">*</span>{/if}</label
	>
	<Combobox.Root
		type={multiple ? 'multiple' : 'single'}
		{items}
		bind:value={value as never}
		bind:open
		{disabled}
		{required}
		onOpenChange={handleOpenChange}
		onValueChange={handleValueChange}
	>
		<div class="control">
			<Search class="combobox-search" size={16} strokeWidth={1.75} aria-hidden="true" />
			{#if multiple && !open && selectedLabels}
				<span class="selected-values" aria-hidden="true">{selectedLabels}</span>
			{/if}
			<Combobox.Input
				{id}
				class="combobox-input"
				{placeholder}
				{disabled}
				aria-invalid={error ? 'true' : undefined}
				aria-describedby={describedBy}
				oninput={handleInput}
			/>
			<Combobox.Trigger class="combobox-trigger" {disabled} aria-label={`Show ${label} options`}>
				<ChevronDown size={16} strokeWidth={1.75} aria-hidden="true" />
			</Combobox.Trigger>
		</div>
		<Combobox.Portal>
			<Combobox.Content class="combobox-content" sideOffset={6}>
				<Combobox.Viewport class="combobox-viewport">
					{#each filteredItems as item (item.value)}
						<Combobox.Item
							class="combobox-item"
							value={item.value}
							label={item.label}
							disabled={item.disabled}
						>
							{#snippet children({ selected }: { selected: boolean })}
								<span>{item.label}</span>
								{#if selected}<Check
										class="combobox-indicator"
										size={15}
										strokeWidth={2}
										aria-hidden="true"
									/>{/if}
							{/snippet}
						</Combobox.Item>
					{:else}
						<p class="empty">No matching options.</p>
					{/each}
				</Combobox.Viewport>
			</Combobox.Content>
		</Combobox.Portal>
	</Combobox.Root>
	{#if description && !error}<p id={descriptionId}>{description}</p>{/if}
	{#if error}<p class="error" id={errorId}>{error}</p>{/if}
</div>

<style>
	.field {
		display: grid;
		align-content: start;
		gap: 0.45rem;
		min-width: 0;
	}
	label {
		color: var(--color-text-muted);
		font-size: var(--text-sm);
	}
	.required {
		margin-left: 0.2rem;
		color: var(--color-danger);
	}
	.control {
		position: relative;
	}
	:global(.combobox-input) {
		width: 100%;
		height: 2.65rem;
		padding: 0.65rem 2.55rem 0.65rem 2.25rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-sm);
		outline: none;
		background: var(--color-surface);
		color: var(--color-text);
		font-size: var(--text-sm);
		transition:
			border-color var(--duration-normal) var(--ease-standard),
			box-shadow var(--duration-normal) var(--ease-standard);
	}
	:global(.combobox-input::placeholder) {
		color: var(--color-text-subtle);
	}
	.has-selection :global(.combobox-input[data-state='closed']) {
		color: transparent;
		caret-color: transparent;
	}
	.selected-values {
		position: absolute;
		top: 50%;
		left: 2.25rem;
		right: 2.55rem;
		overflow: hidden;
		color: var(--color-text);
		font-size: var(--text-sm);
		white-space: nowrap;
		pointer-events: none;
		text-overflow: ellipsis;
		transform: translateY(-50%);
	}
	:global(.combobox-input:hover:not(:disabled)) {
		border-color: var(--color-accent-muted);
	}
	:global(.combobox-input:focus) {
		border-color: var(--color-border-focus);
		box-shadow: var(--focus-ring);
	}
	:global(.combobox-input:disabled) {
		cursor: not-allowed;
		opacity: 0.5;
	}
	:global(.combobox-search) {
		position: absolute;
		top: 50%;
		left: 0.75rem;
		z-index: 1;
		color: var(--color-text-subtle);
		pointer-events: none;
		transform: translateY(-50%);
	}
	:global(.combobox-trigger) {
		position: absolute;
		top: 0;
		right: 0;
		display: grid;
		width: 2.5rem;
		height: 100%;
		place-items: center;
		border: 0;
		outline: none;
		background: transparent;
		color: var(--color-text-subtle);
		cursor: pointer;
	}
	:global(.combobox-trigger:focus-visible) {
		color: var(--color-accent);
	}
	:global(.combobox-trigger:disabled) {
		cursor: not-allowed;
	}
	:global(.combobox-content) {
		z-index: var(--z-dropdown);
		width: var(--bits-combobox-anchor-width);
		min-width: var(--bits-combobox-anchor-width);
		max-height: min(18rem, var(--bits-combobox-content-available-height));
		overflow: hidden;
		padding: 0.35rem;
		border: 1px solid var(--color-border-strong);
		border-radius: var(--radius-md);
		background: var(--color-surface-raised);
		box-shadow: var(--shadow-md);
	}
	:global(.combobox-viewport) {
		max-height: calc(min(18rem, var(--bits-combobox-content-available-height)) - 0.7rem);
		overflow: auto;
	}
	:global(.combobox-item) {
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
	:global(.combobox-item[data-highlighted]) {
		background: var(--color-surface-hover);
		color: var(--color-text);
	}
	:global(.combobox-item[data-disabled]) {
		cursor: not-allowed;
		opacity: 0.45;
	}
	:global(.combobox-indicator) {
		color: var(--color-accent);
	}
	.empty,
	.field > p {
		max-width: none;
		font-size: var(--text-xs);
		line-height: 1.45;
		color: var(--color-text-subtle);
	}
	.empty {
		padding: 0.65rem;
	}
	.error {
		color: var(--color-danger) !important;
	}
	.error-state :global(.combobox-input) {
		border-color: color-mix(in srgb, var(--color-danger), transparent 35%);
	}
</style>
