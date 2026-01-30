<script lang="ts">
	import { Instagram, Linkedin, Twitter, Youtube } from 'lucide-svelte';

	const brand = 'GuikiPT';
	const navLinks = [
		{ href: '/', label: 'Home' },
		{ href: '/about', label: 'About' },
		{ href: '/projects', label: 'Projects' },
		{ href: '/contact', label: 'Contact' }
	];
	const socials = [
		{ href: 'https://www.linkedin.com', label: 'LinkedIn', icon: Linkedin, color: '#0A66C2', glow: 'rgba(10, 102, 194, 0.85)' },
		{ href: 'https://twitter.com', label: 'Twitter', icon: Twitter, color: '#1DA1F2', glow: 'rgba(29, 161, 242, 0.85)' },
		{ href: 'https://www.instagram.com', label: 'Instagram', icon: Instagram, color: '#E4405F', glow: 'rgba(228, 64, 95, 0.85)' },
		{ href: 'https://www.youtube.com', label: 'YouTube', icon: Youtube, color: '#FF0000', glow: 'rgba(255, 0, 0, 0.85)' }
	];

	let mobileMenuOpen = $state(false);
</script>

<header class="w-full bg-black">
	<div class="navbar-wrapper">
		<nav
			class="navbar relative flex w-full items-center justify-between bg-black px-4 text-white lg:mx-auto lg:w-3/4"
		>
			<div class="relative z-10 navbar-start flex items-center">
				<div class="dropdown">
					<button
						tabindex="0"
						class="btn btn-circle btn-ghost lg:hidden"
						aria-label="Toggle mobile menu"
						onclick={() => (mobileMenuOpen = !mobileMenuOpen)}
					>
						<svg
							xmlns="http://www.w3.org/2000/svg"
							class="h-5 w-5"
							fill="none"
							viewBox="0 0 24 24"
							stroke="currentColor"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M4 6h16M4 12h16M4 18h7"
							/>
						</svg>
					</button>
					{#if mobileMenuOpen}
						<ul
							tabindex="-1"
							class="dropdown-content menu z-1 mt-3 w-52 menu-sm rounded-box bg-base-200 p-2 shadow"
						>
							{#each navLinks as link (link.href)}
								<li><a href={link.href}>{link.label}</a></li>
							{/each}
						</ul>
					{/if}
				</div>
				<ul class="menu menu-horizontal hidden px-1 lg:flex">
					{#each navLinks as link (link.href)}
						<li><a href={link.href}>{link.label}</a></li>
					{/each}
				</ul>
			</div>
			<div class="relative z-10 navbar-center">
				<a href="/" class="notch-title">{brand}</a>
			</div>
			<div class="relative z-10 navbar-end">
				<div class="flex items-center gap-3">
					{#each socials as social (social.label)}
						{@const Icon = social.icon}
						<a
							href={social.href}
							target="_blank"
							rel="noreferrer"
							aria-label={social.label}
							class="btn btn-circle btn-ghost social-link"
							style="--glow: {social.glow}"
						>
							<Icon size={20} style="color: {social.color}" />
						</a>
					{/each}
				</div>
			</div>
		</nav>
	</div>
</header>

<style>
	.navbar-wrapper {
		display: flex;
		justify-content: center;
	}

	nav {
		border-left: 1px solid #f97316;
		border-right: 1px solid #f97316;
		border-bottom: 1px solid #f97316;
		border-radius: 0 0 24px 24px;
		box-shadow: 0 0 45px rgba(249, 115, 22, 0.55);
	}

	.notch-title {
		font-family: 'Bungee Shade', sans-serif;
		font-size: 1.5rem;
		line-height: 1;
		color: #fb923c;
		text-shadow:
			0 0 10px rgba(249, 115, 22, 0.6),
			0 0 20px rgba(249, 115, 22, 0.4);
	}

	.navbar-start .menu a {
		color: #e5e7eb;
		padding: 0.35rem 0.75rem;
		border-radius: 9999px;
		transition:
			color 150ms ease,
			background-color 150ms ease,
			box-shadow 150ms ease,
			transform 150ms ease;
	}

	.navbar-start .menu a:hover {
		color: #fff7ed;
		background: rgba(249, 115, 22, 0.18);
		box-shadow:
			0 0 10px rgba(249, 115, 22, 0.6),
			0 0 20px rgba(249, 115, 22, 0.4);
		transform: translateY(-1px);
	}

	.navbar-start .menu a:focus-visible {
		outline: 2px solid rgba(249, 115, 22, 0.8);
		outline-offset: 2px;
	}

	.navbar-end a[aria-label='LinkedIn'] {
		filter: drop-shadow(0 0 12px var(--glow)) drop-shadow(0 0 6px var(--glow));
	}

	.navbar-end a[aria-label='Twitter'] {
		filter: drop-shadow(0 0 12px var(--glow)) drop-shadow(0 0 6px var(--glow));
	}

	.navbar-end a[aria-label='Instagram'] {
		filter: drop-shadow(0 0 12px var(--glow)) drop-shadow(0 0 6px var(--glow));
	}

	.navbar-end a[aria-label='YouTube'] {
		filter: drop-shadow(0 0 12px var(--glow)) drop-shadow(0 0 6px var(--glow));
	}

	@media (min-width: 1024px) {
		.notch-title {
			font-size: 2rem;
		}
	}
</style>
