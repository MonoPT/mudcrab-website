<section class="full-bleed">
	<h1>Mudcrab</h1>
</section>

<p><a href="/components">Check components</a></p>

<style>
	section {
		min-height: 60svh;
		padding: 4.5rem max(1rem, calc((100vw - var(--content-wide)) / 2)) 2rem;
		background-image:
			linear-gradient(to right, var(--color-background) 0%, transparent 65%),
			linear-gradient(to bottom, var(--color-background) 0%, transparent 40%),
			url('/wallpapers/0.jpg');
		background-size: cover;
		background-position: center;
	}

	.full-bleed {
		width: 100vw;
		margin-inline: calc(50% - 50vw);
	}

	@media (max-width: 700px) {
		section {
			padding-top: 4rem;
		}
	}
</style>
