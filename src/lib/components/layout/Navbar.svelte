<script lang="ts">
	import { onMount } from 'svelte';

	// Icon Components
	const Instagram = ({ size = 24, style = '' }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="${style}"><rect x="2" y="2" width="20" height="20" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/><line x1="17.5" y1="6.5" x2="17.51" y2="6.5"/></svg>`;
	const Linkedin = ({ size = 24, style = '' }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="${style}"><path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"/><rect x="2" y="9" width="4" height="12"/><circle cx="4" cy="4" r="2"/></svg>`;
	const Twitter = ({ size = 24, style = '' }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="${style}"><path d="M22 4s-.7 2.1-2 3.4c1.6 10-9.4 17.3-18 11.6 2.2.1 4.4-.6 6-2C3 15.5.5 9.6 3 5c2.2 2.6 5.6 4.1 9 4-.9-4.2 4-6.6 7-3.8 1.1 0 3-1.2 3-1.2z"/></svg>`;
	const Youtube = ({ size = 24, style = '' }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="${style}"><path d="M22.54 6.42a2.78 2.78 0 0 0-1.94-2C18.88 4 12 4 12 4s-6.88 0-8.6.46a2.78 2.78 0 0 0-1.94 2A29 29 0 0 0 1 11.75a29 29 0 0 0 .46 5.33A2.78 2.78 0 0 0 3.4 19c1.72.46 8.6.46 8.6.46s6.88 0 8.6-.46a2.78 2.78 0 0 0 1.94-2 29 29 0 0 0 .46-5.25 29 29 0 0 0-.46-5.33z"/><polygon points="9.75 15.02 15.5 11.75 9.75 8.48 9.75 15.02"/></svg>`;

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

	let sidebarOpen = $state(false);
	let showNavbar = $state(true);
	let lastScrollY = 0;

	function closeSidebar() {
		sidebarOpen = false;
	}

	onMount(() => {
		const handleScroll = () => {
			const currentScrollY = window.scrollY;
			
			if (currentScrollY < 10) {
				showNavbar = true;
			} else if (currentScrollY > lastScrollY) {
				// Scrolling down
				showNavbar = false;
			} else {
				// Scrolling up
				showNavbar = true;
			}
			
			lastScrollY = currentScrollY;
		};

		window.addEventListener('scroll', handleScroll, { passive: true });

		return () => {
			window.removeEventListener('scroll', handleScroll);
		};
	});
</script>

<header class="w-full bg-black navbar-header" class:hidden={!showNavbar}>
	<div class="drawer">
		<input
			id="nav-drawer"
			type="checkbox"
			class="drawer-toggle"
			bind:checked={sidebarOpen}
		/>
		<div class="drawer-content">
			<div class="navbar-wrapper">
				<nav
					class="navbar relative flex w-full items-center justify-between bg-black px-4 text-white lg:mx-auto lg:w-3/4"
				>
					<div class="relative z-10 navbar-start flex items-center">
						<label
							for="nav-drawer"
							class="btn btn-circle btn-ghost lg:hidden hamburger-btn"
							aria-label="Toggle sidebar"
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
						</label>
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
						<div class="hidden lg:flex items-center gap-3">
							{#each socials as social (social.label)}
								<a
									href={social.href}
									target="_blank"
									rel="noreferrer"
									aria-label={social.label}
									class="btn btn-circle btn-ghost social-link"
									style="--glow: {social.glow}"
								>
									{@html social.icon({ size: 20, style: `color: ${social.color}` })}
								</a>
							{/each}
						</div>
					</div>
				</nav>
			</div>
		</div>
		<div class="drawer-side z-50">
			<label
				for="nav-drawer"
				class="drawer-overlay"
				aria-label="Close sidebar"
			></label>
			<ul class="menu min-h-full w-64 bg-black border-r border-orange-500 p-6 sidebar-menu">
				<li class="mb-6">
					<h3 class="sidebar-brand">{brand}</h3>
				</li>
				<li class="sidebar-divider"></li>
				{#each navLinks as link (link.href)}
					<li>
						<a
							href={link.href}
							onclick={closeSidebar}
							class="sidebar-link"
						>
							{link.label}
						</a>
					</li>
				{/each}
				<li class="sidebar-divider mt-6"></li>
				<li class="mb-3 mt-4 text-xs font-semibold uppercase text-gray-400">Social</li>
				<div class="flex gap-3 px-2">
					{#each socials as social (social.label)}
						<a
							href={social.href}
							target="_blank"
							rel="noreferrer"
							aria-label={social.label}
							class="sidebar-social-link"
							style="--icon: {social.color}; --glow: {social.glow}"
						>
							{@html social.icon({ size: 20 })}
						</a>
					{/each}
				</div>
			</ul>
		</div>
	</div>
</header>

<style>
	.navbar-header {
		position: fixed;
		top: 0;
		left: 0;
		right: 0;
		transition: 
			transform 0.7s cubic-bezier(0.4, 0, 0.2, 1),
			opacity 0.7s cubic-bezier(0.4, 0, 0.2, 1);
		z-index: 100;
		opacity: 1;
	}

	.navbar-header.hidden {
		transform: translateY(-100%);
		opacity: 0;
	}

	.navbar-wrapper {
		display: flex;
		justify-content: center;
	}

	header {
		position: relative;
		z-index: 100;
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
		color: #fb923c;
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

	/* Sidebar Styles */
	.sidebar-menu {
		box-shadow: 4px 0 45px rgba(249, 115, 22, 0.55);
	}

	.sidebar-brand {
		font-family: 'Bungee Shade', sans-serif;
		font-size: 1.25rem;
		line-height: 1;
		color: #fb923c;
		text-shadow:
			0 0 10px rgba(249, 115, 22, 0.6),
			0 0 20px rgba(249, 115, 22, 0.4);
		padding: 0;
		background: none !important;
	}

	.sidebar-divider {
		height: 1px;
		background: linear-gradient(90deg, #f97316 0%, transparent 100%);
		margin: 0.5rem 0;
		padding: 0;
	}

	.sidebar-link {
		color: #fb923c !important;
		padding: 0.5rem 1rem !important;
		border-radius: 0.5rem !important;
		transition:
			all 150ms ease !important;
		background: none !important;
	}

	.sidebar-link:hover {
		color: #fff7ed !important;
		background: rgba(249, 115, 22, 0.18) !important;
		box-shadow:
			0 0 10px rgba(249, 115, 22, 0.6),
			0 0 20px rgba(249, 115, 22, 0.4) !important;
		transform: translateX(4px);
	}

	.sidebar-social-link {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 2.5rem;
		height: 2.5rem;
		border-radius: 50%;
		color: var(--icon);
		transition: all 150ms ease;
		filter: drop-shadow(0 0 8px var(--glow));
	}

	.sidebar-social-link:hover {
		transform: scale(1.1);
		filter: drop-shadow(0 0 12px var(--glow)) drop-shadow(0 0 6px var(--glow));
	}

	.hamburger-btn svg {
		stroke: #fb923c;
	}

	.hamburger-btn:hover svg {
		stroke: #fff7ed;
	}

	@media (min-width: 1024px) {
		.notch-title {
			font-size: 2rem;
		}
	}
</style>
