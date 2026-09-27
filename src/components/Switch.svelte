<script lang="ts">
	import { Switch, useId } from 'bits-ui';

	let {
		id = useId(),
		label,
		description,
		checked = $bindable(false),
		disabled = false,
		required = false
	}: {
		id?: string;
		label: string;
		description?: string;
		checked?: boolean;
		disabled?: boolean;
		required?: boolean;
	} = $props();
</script>

<div class="switch-field">
	<Switch.Root
		{id}
		bind:checked
		{disabled}
		{required}
		aria-labelledby={`${id}-label`}
		aria-describedby={description ? `${id}-description` : undefined}
		class="switch"
	>
		<span class="thumb" aria-hidden="true"></span>
	</Switch.Root>
	<div class="copy">
		<label id={`${id}-label`} for={id}>{label}</label>
		{#if description}<p id={`${id}-description`}>{description}</p>{/if}
	</div>
</div>

<style>
	.switch-field {
		display: flex;
		align-items: flex-start;
		gap: 0.75rem;
		min-width: 0;
	}
	:global(.switch) {
		display: inline-flex;
		flex: 0 0 auto;
		align-items: center;
		width: 2.75rem;
		height: 1.5rem;
		margin-top: 0.05rem;
		padding: 0.15rem;
		border: 1px solid var(--color-border-strong);
		border-radius: 999px;
		outline: none;
		background: var(--color-surface);
		cursor: pointer;
		transition:
			border-color var(--duration-normal) var(--ease-standard),
			background var(--duration-normal) var(--ease-standard),
			box-shadow var(--duration-normal) var(--ease-standard);
	}
	:global(.switch:hover:not(:disabled)) {
		border-color: var(--color-accent);
	}
	:global(.switch:focus-visible) {
		border-color: var(--color-border-focus);
		box-shadow: var(--focus-ring);
	}
	:global(.switch[data-state='checked']) {
		justify-content: flex-end;
		border-color: var(--color-accent);
		background: var(--color-accent);
	}
	:global(.switch:disabled) {
		cursor: not-allowed;
		opacity: 0.45;
	}
	.thumb {
		display: block;
		width: 1.1rem;
		height: 1.1rem;
		border-radius: 50%;
		background: var(--color-text-muted);
		box-shadow: var(--shadow-sm);
		transition:
			background var(--duration-normal) var(--ease-standard),
			transform var(--duration-normal) var(--ease-standard);
	}
	:global(.switch[data-state='checked']) .thumb {
		background: var(--color-accent-ink);
	}
	.copy {
		display: grid;
		gap: 0.25rem;
		min-width: 0;
	}
	label {
		color: var(--color-text-muted);
		font-size: var(--text-sm);
		line-height: 1.4;
		cursor: pointer;
	}
	p {
		max-width: none;
		font-size: var(--text-xs);
		line-height: 1.45;
	}
</style>
