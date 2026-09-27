<script lang="ts">
	import { AlertTriangle, ArrowRight, Check, Download, Info, Plus, X } from '@lucide/svelte';
	import Button from '../../components/Button.svelte';
		import Link from '../../components/Link.svelte';
			import Badge from '../../components/Badge.svelte';
</script>

{#snippet arrowIcon()}
	<ArrowRight size={16} strokeWidth={1.75} />
{/snippet}

{#snippet downloadIcon()}
	<Download size={16} strokeWidth={1.75} />
{/snippet}

{#snippet infoIcon()}
	<Info size={14} strokeWidth={1.75} />
{/snippet}

{#snippet successIcon()}
	<Check size={14} strokeWidth={1.75} />
{/snippet}

{#snippet warningIcon()}
	<AlertTriangle size={14} strokeWidth={1.75} />
{/snippet}

<svelte:head>
	<title>Components — Mudcrab</title>
	<meta
		name="description"
		content="Mudcrab design system component showcase and typography reference."
	/>
</svelte:head>

<div class="showcase">
	<header class="hero">
		<div class="hero-mark" aria-hidden="true">ᛉ</div>
		<div>
			<p class="eyebrow">Mudcrab · Design system</p>
			<h1>Components</h1>
			<p class="hero-copy">
				A reusable component library for a clear, immersive interface inspired by Skyrim's
				quiet, weathered UI language.
			</p>
		</div>
	</header>

	<div class="rule" aria-hidden="true"></div>

	<main>
		<section class="section" aria-labelledby="typography-heading">
			<div class="section-heading">
				<p class="eyebrow">01 · Foundations</p>
				<h2 id="typography-heading">Typography</h2>
				<p>
					Cinzel brings an engraved, considered voice to headings. Inter keeps body copy,
					menus, labels, and controls practical and readable.
				</p>
			</div>

			<div class="specimen-grid">
				<div class="type-specimen">
					<div class="type-row">
						<span class="type-label">H1 · 3xl</span>
						<h1>The Elder Scrolls V</h1>
					</div>
					<div class="type-row">
						<span class="type-label">H2 · 2xl</span>
						<h2>A better way to play</h2>
					</div>
					<div class="type-row">
						<span class="type-label">H3 · xl</span>
						<h3>Thoughtful improvements</h3>
					</div>
					<div class="type-row">
						<span class="type-label">H4 · lg</span>
						<h4>Streamlined, familiar, powerful</h4>
					</div>
					<div class="type-row">
						<span class="type-label">H5 · md</span>
						<h5>Designed for immersion</h5>
					</div>
					<div class="type-row">
						<span class="type-label">H6 · sm</span>
						<h6>Feature overview</h6>
					</div>
				</div>

				<aside class="type-notes">
					<div class="note">
						<span class="type-label">Body</span>
						<p>
							Mudcrab enhances Skyrim's user interface with a calmer visual rhythm,
							clearer hierarchy, and a more immersive reading experience.
						</p>
					</div>
					<div class="note">
						<span class="type-label">Lead</span>
						<p class="lead">Clarity without breaking immersion.</p>
					</div>
					<div class="note">
						<span class="type-label">Utilities</span>
						<p class="eyebrow">Eyebrow / overline</p>
						<p class="small">Small supporting text for metadata and secondary content.</p>
						<p class="caption">Caption · Updated 2 days ago</p>
					</div>
				</aside>
			</div>
		</section>

		<section class="section" aria-labelledby="buttons-heading">
			<div class="section-heading">
				<p class="eyebrow">02 · Actions</p>
				<h2 id="buttons-heading">Buttons</h2>
				<p>One button component covers text actions, loading states, and icon-only controls.</p>
			</div>

			<div class="button-showcase">
				<div class="button-group">
					<span class="type-label">Variants</span>
					<div class="button-row">
						<Button variant="primary" trailing={arrowIcon}>Get started</Button>
						<Button variant="secondary">View details</Button>
						<Button variant="ghost">Explore</Button>
						<Button variant="danger">Remove</Button>
					</div>
				</div>

				<div class="button-group">
					<span class="type-label">With Lucide icons</span>
					<div class="button-row">
						<Button variant="secondary" leading={downloadIcon}>Download</Button>
						<Button variant="button" label="Add item"><Plus size={17} strokeWidth={1.75} /></Button>
						<Button variant="button" label="Close"><X size={17} strokeWidth={1.75} /></Button>
						<Button variant="button" label="Next" size="sm"><ArrowRight size={15} strokeWidth={1.75} /></Button>
					</div>
				</div>

				<div class="button-group">
					<span class="type-label">States and sizes</span>
					<div class="button-row">
						<Button size="sm" variant="secondary">Small</Button>
						<Button size="lg" variant="primary">Large</Button>
						<Button variant="secondary" loading>Saving</Button>
						<Button variant="secondary" disabled>Disabled</Button>
					</div>
				</div>
			</div>
		</section>

		<section class="section" aria-labelledby="links-heading">
			<div class="section-heading">
				<p class="eyebrow">03 · Navigation</p>
				<h2 id="links-heading">Links</h2>
				<p>Links carry navigation and inline reading actions without competing with primary buttons.</p>
			</div>

			<div class="link-showcase">
				<div class="link-example">
					<span class="type-label">Default link</span>
					<Link href="/components" arrow>Read more</Link>
				</div>
				<div class="link-example">
					<span class="type-label">Hover / muted</span>
					<Link href="/components" variant="muted" arrow>View details</Link>
				</div>
				<div class="link-example">
					<span class="type-label">External link</span>
					<Link href="https://github.com" external>View on GitHub</Link>
				</div>
				<div class="link-example">
					<span class="type-label">Inline link</span>
					<p>Read the <Link href="/components" variant="inline" underline={false}>component documentation</Link> to learn more.</p>
				</div>
			</div>
		</section>

		<section class="section" aria-labelledby="badges-heading">
			<div class="section-heading">
				<p class="eyebrow">04 · Metadata</p>
				<h2 id="badges-heading">Badges</h2>
				<p>Compact labels make status, category, and environment information easy to scan.</p>
			</div>

			<div class="badge-showcase">
				<div class="badge-group">
					<span class="type-label">Tones</span>
					<div class="badge-row">
						<Badge>Neutral</Badge>
						<Badge tone="accent">Accent</Badge>
						<Badge tone="success" icon={successIcon}>Success</Badge>
						<Badge tone="warning" icon={warningIcon}>Warning</Badge>
						<Badge tone="danger">Danger</Badge>
					</div>
				</div>
				<div class="badge-group">
					<span class="type-label">Sizes and context</span>
					<div class="badge-row">
						<Badge size="md" tone="accent" icon={infoIcon}>Development</Badge>
						<Badge size="md" tone="success" icon={successIcon}>Installed</Badge>
						<Badge size="sm">Version 1.0</Badge>
					</div>
				</div>
			</div>
		</section>

		<section class="section tokens" aria-labelledby="tokens-heading">
			<div class="section-heading">
				<p class="eyebrow">05 · Usage</p>
				<h2 id="tokens-heading">Semantic HTML first</h2>
				<p>Use the correct heading level for the document structure. The theme handles the visual hierarchy.</p>
			</div>
			<div class="token-grid">
				<div class="token-card"><code>&lt;h1&gt;</code><span>Page title</span></div>
				<div class="token-card"><code>&lt;h2&gt;</code><span>Major section</span></div>
				<div class="token-card"><code>&lt;h3&gt;</code><span>Component group</span></div>
				<div class="token-card"><code>&lt;p&gt;</code><span>Body content</span></div>
			</div>
		</section>
	</main>

	<footer>
		<span class="eyebrow">Next</span>
		<p>Links, cards, and form controls will be added here as they are developed.</p>
	</footer>
</div>

<style>
	.showcase { width: min(100% - 2rem, var(--content-wide)); margin: 0 auto; padding: clamp(2rem, 7vw, 6rem) 0; }
	.hero { display: flex; align-items: center; gap: 1.5rem; max-width: 48rem; }
	.hero-mark { display: grid; width: 4.5rem; height: 4.5rem; flex: 0 0 auto; place-items: center; border: 1px solid var(--color-border-strong); color: var(--color-accent); font: 2.5rem var(--font-display); transform: rotate(45deg); }
	.hero-mark::first-letter { display: block; transform: rotate(-45deg); }
	.hero h1 { margin-top: .4rem; }
	.hero-copy { margin-top: 1.25rem; max-width: 42rem; font-size: var(--text-lg); }
	.eyebrow { margin-bottom: .7rem; }
	.rule { height: 1px; margin: clamp(2.5rem, 8vw, 6rem) 0; background: linear-gradient(90deg, var(--color-border), transparent); }
	.section + .section { margin-top: clamp(4rem, 10vw, 8rem); }
	.section-heading { max-width: 42rem; margin-bottom: 2.5rem; }
	.section-heading h2 { margin-bottom: 1rem; }
	.specimen-grid { display: grid; grid-template-columns: minmax(0, 1.5fr) minmax(16rem, .75fr); gap: 1px; border: 1px solid var(--color-border); background: var(--color-border); }
	.type-specimen, .type-notes { background: var(--color-surface); }
	.type-row { display: grid; grid-template-columns: 6rem 1fr; align-items: baseline; gap: 1rem; padding: 1.35rem 1.5rem; border-bottom: 1px solid var(--color-border); }
	.type-row:last-child { border-bottom: 0; }
	.type-label { display: block; color: var(--color-text-subtle); font: 600 var(--text-xs) var(--font-body); letter-spacing: var(--tracking-label); text-transform: uppercase; }
	.type-notes { display: grid; align-content: start; }
	.note { padding: 1.5rem; border-bottom: 1px solid var(--color-border); }
	.note:last-child { border-bottom: 0; }
	.note > :not(.type-label) { margin-top: .75rem; }
	.note .eyebrow { color: var(--color-text-muted); }
	.note .caption { margin-top: .9rem; }
	.tokens { padding-top: 1px; }
	.button-showcase { display: grid; gap: 1px; border: 1px solid var(--color-border); background: var(--color-border); }
	.link-showcase { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1px; border: 1px solid var(--color-border); background: var(--color-border); }
	.badge-showcase { display: grid; gap: 1px; border: 1px solid var(--color-border); background: var(--color-border); }
	.badge-group { display: grid; gap: 1rem; padding: 1.5rem; background: var(--color-surface); }
	.badge-row { display: flex; flex-wrap: wrap; align-items: center; gap: .75rem; }
	.link-example { display: grid; align-content: start; gap: 1rem; min-height: 8rem; padding: 1.5rem; background: var(--color-surface); }
	.link-example p { font-size: var(--text-sm); }
	.link-example :global(.link) { display: inline-flex; }
	.button-group { display: grid; gap: 1rem; padding: 1.5rem; background: var(--color-surface); }
	.button-row { display: flex; flex-wrap: wrap; align-items: center; gap: .75rem; }
	.token-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: .75rem; }
	.token-card { display: grid; gap: .65rem; padding: 1.25rem; border: 1px solid var(--color-border); border-radius: var(--radius-md); background: var(--color-surface); }
	.token-card code { color: var(--color-accent); font: .85rem var(--font-mono); }
	.token-card span { color: var(--color-text-muted); font-size: var(--text-sm); }
	footer { display: flex; gap: 1rem; align-items: baseline; margin-top: clamp(4rem, 10vw, 8rem); padding-top: 1.5rem; border-top: 1px solid var(--color-border); }
	footer .eyebrow { flex: 0 0 auto; margin: 0; }
	footer p { font-size: var(--text-sm); }
	@media (max-width: 700px) { .showcase { width: min(100% - 1.5rem, var(--content-wide)); } .hero { align-items: flex-start; } .hero-mark { width: 3.25rem; height: 3.25rem; font-size: 1.75rem; } .specimen-grid { grid-template-columns: 1fr; } .link-showcase { grid-template-columns: repeat(2, 1fr); } .token-grid { grid-template-columns: repeat(2, 1fr); } .type-row { grid-template-columns: 4.5rem 1fr; padding-inline: 1rem; } footer { display: block; } footer p { margin-top: .75rem; } }
	@media (max-width: 420px) { .type-row { grid-template-columns: 1fr; gap: .5rem; } .link-showcase { grid-template-columns: 1fr; } .token-grid { grid-template-columns: 1fr; } }
</style>
