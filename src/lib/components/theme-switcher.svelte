<script lang="ts">
	import { theme } from '$lib/app';
	let clazz = '';
	export { clazz as class };

	const on_change = (event: Event) => {
		const target = event.target as HTMLInputElement;
		const new_theme = target.checked ? 'dark' : 'light';
		theme.set(new_theme);
	};
</script>

<label class={clazz}>
	<input
		name="theme"
		type="checkbox"
		checked={$theme === 'dark'}
		on:change|preventDefault={on_change}
	/>
	<span class="switch" />
	<span class="visually-hidden">Toggle "dark theme"</span>
</label>

<style>
	label {
		--size-w: calc(var(--hitarea-size) * 2);
		--size-h: var(--hitarea-size);

		display: flex;
		position: relative;
		align-items: center;
		cursor: pointer;
		gap: 0.75rem;
	}

	label,
	:global(.light) label {
		--icon: url(/icons/lightbulb.svg);
	}
	@media (prefers-color-scheme: dark) {
		label {
			--icon: url(/icons/lightbulb_inverted.svg);
		}
	}
	:global(.dark) label {
		--icon: url(/icons/lightbulb_inverted.svg);
	}

	label::before {
		content: '';
		position: absolute;
		top: 50%;
		left: 50%;
		width: var(--size-w);
		height: var(--size-h);
		transform: translate(-50%, -50%);
	}

	label::after {
		content: '';
		display: block;
		height: 1rem;
		width: 1rem;
		background-image: var(--icon);
	}

	input {
		display: none;
	}

	.switch {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 2.5rem;
		height: 1.5rem;
		background-color: var(--theme-track);
		border-radius: 1rem;
	}

	.switch::before {
		content: '';
		display: block;
		width: 1rem;
		height: 1rem;
		border-radius: 100%;
		background-color: var(--theme-fg);
		transform: translateX(50%);

		transition-property: transform, background-color;
		transition-duration: 200ms, 200ms;
		transition-timing-function: ease-in-out;
	}

	@media (min-width: 55em) {
		label:hover .switch::before {
			background-color: var(--theme-accent);
		}
	}

	input:checked + .switch::before {
		transform: translateX(-50%);
	}
</style>
