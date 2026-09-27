<script lang="ts">
	let {
		id = 'text-input',
		label,
		value = $bindable(''),
		placeholder,
		type = 'text',
		description,
		error,
		disabled = false,
		required = false
	}: {
		id?: string;
		label: string;
		value?: string;
		placeholder?: string;
		type?: 'text' | 'search' | 'password' | 'email';
		description?: string;
		error?: string;
		disabled?: boolean;
		required?: boolean;
	} = $props();

	let descriptionId = $derived(description ? `${id}-description` : undefined);
	let errorId = $derived(error ? `${id}-error` : undefined);
	let describedBy = $derived([descriptionId, errorId].filter(Boolean).join(' ') || undefined);
</script>

<div class="field" class:error-state={error}>
	<label for={id}>{label}{#if required}<span class="required" aria-hidden="true">*</span>{/if}</label>
	<input
		{id}
		{type}
		{placeholder}
		bind:value
		{disabled}
		{required}
		aria-invalid={error ? 'true' : undefined}
		aria-describedby={describedBy}
	/>
	{#if description && !error}<p id={descriptionId}>{description}</p>{/if}
	{#if error}<p class="error" id={errorId}>{error}</p>{/if}
</div>

<style>
	.field { display: grid; align-content: start; gap: 0.45rem; min-width: 0; }
	label { color: var(--color-text-muted); font-size: var(--text-sm); }
	.required { margin-left: 0.2rem; color: var(--color-danger); }
	input { width: 100%; height: 2.65rem; min-height: 2.65rem; padding: 0.65rem 0.8rem; border: 1px solid var(--color-border-strong); border-radius: var(--radius-sm); outline: none; background: var(--color-surface); color: var(--color-text); font-size: var(--text-sm); transition: border-color var(--duration-normal) var(--ease-standard), box-shadow var(--duration-normal) var(--ease-standard); }
	input::placeholder { color: var(--color-text-subtle); }
	input:hover:not(:disabled) { border-color: var(--color-accent-muted); }
	input:focus { border-color: var(--color-border-focus); box-shadow: var(--focus-ring); }
	.field p { max-width: none; font-size: var(--text-xs); line-height: 1.45; color: var(--color-text-subtle); }
	.error { color: var(--color-danger) !important; }
	.error-state input { border-color: color-mix(in srgb, var(--color-danger), transparent 35%); }
	input:disabled { cursor: not-allowed; opacity: 0.5; }
</style>
