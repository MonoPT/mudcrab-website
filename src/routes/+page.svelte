<script lang="ts">
	import Button from '../components/Button.svelte';
</script>

{#snippet githubIcon()}
	<img src="https://cdn.simpleicons.org/github" alt="" aria-hidden="true" />
{/snippet}

{#snippet discordIcon()}
	<img src="https://cdn.simpleicons.org/discord" alt="" aria-hidden="true" />
{/snippet}

<section class="full-bleed heroSection">
	<h1>Mudcrab</h1>
	<h2>The same game, rebuilt for a seamless new world.</h2>
	<p>
		Mudcrab is being remade in Bevy from the ground up: a new engine, Luau scripting, and an open
		world with no loading screens. Explore farther, build more, and make the world your own.
	</p>
	<div class="actions">
		<Button
			variant="primary"
			href="https://github.com/realfakenerd/mudcrab"
			target="_blank"
			leading={githubIcon}>GitHub</Button
		>
		<Button variant="secondary" href="https://discord.gg/SnACRkduR" target="_blank" leading={discordIcon}>Discord</Button>
	</div>
</section>

<p><a href="/components">Check components</a></p>

<style>
	section.heroSection {
		min-height: 60svh;
		padding: 4.5rem max(1rem, calc((100vw - var(--content-wide)) / 2)) 2rem;
		background-image:
			linear-gradient(to right, var(--color-background) 0%, transparent 65%),
			linear-gradient(to bottom, var(--color-background) 0%, transparent 40%),
			url('/wallpapers/0.jpg');
		background-size: cover;
		background-position: center;

		display: flex;
	    flex-direction: column;
		justify-content: center;
	}

	.full-bleed {
		width: 100vw;
		margin-inline: calc(50% - 50vw);
	}

	h1 {
		max-width: 12ch;
		margin: 0;
		font-size: clamp(3rem, 7vw, 5.75rem);
		line-height: 0.9;
	}

	h2 {
		max-width: 22ch;
		margin: 1rem 0 0;
		font-size: clamp(1.2rem, 2vw, 1.7rem);
		line-height: 1.15;
	}

	section > p {
		max-width: 60ch;
		margin: 1.25rem 0 0;
		font-size: clamp(1rem, 1.2vw, 1.1rem);
		line-height: 1.6;
	}

	.actions {
		display: flex;
		flex-wrap: wrap;
		gap: 0.75rem;
		margin-top: 1.5rem;
	}


	@media (max-width: 700px) {
		section {
			padding-top: 4rem;
		}
	}
</style>
