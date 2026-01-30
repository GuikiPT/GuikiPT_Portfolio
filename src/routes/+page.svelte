<script lang="ts">
	import Particles, { particlesInit } from '@tsparticles/svelte';
	import { loadSlim } from '@tsparticles/slim';
	import { onMount } from 'svelte';

	// Icon Components
	const Code = ({ size = 24 }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="16 18 22 12 16 6"/><polyline points="8 6 2 12 8 18"/></svg>`;
	const Briefcase = ({ size = 24 }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="7" width="20" height="14" rx="2" ry="2"/><path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"/></svg>`;
	const Mail = ({ size = 24 }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/><polyline points="22,6 12,13 2,6"/></svg>`;
	const Lightbulb = ({ size = 24 }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 18h6"/><path d="M10 22h4"/><path d="M15.09 14c.18-.98.65-1.74 1.41-2.5A4.65 4.65 0 0 0 18 8 6 6 0 0 0 6 8c0 1 .23 2.23 1.5 3.5A4.61 4.61 0 0 1 8.91 14"/></svg>`;
	const Rocket = ({ size = 24 }) => `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4.5 16.5c-1.5 1.26-2 5-2 5s3.74-.5 5-2c.71-.84.7-2.13-.09-2.91a2.18 2.18 0 0 0-2.91-.09z"/><path d="m12 15-3-3a22 22 0 0 1 2-3.95A12.88 12.88 0 0 1 22 2c0 2.72-.78 7.5-6 11a22.35 22.35 0 0 1-4 2z"/><path d="M9 12H4s.55-3.03 2-4c1.62-1.08 5 0 5 0"/><path d="M12 15v5s3.03-.55 4-2c1.08-1.62 0-5 0-5"/></svg>`;

	let heroVisible = $state(true);
	let aboutVisible = $state(false);
	let abilitiesVisible = $state(false);

	let particlesConfig = {
		particles: {
			number: {
				value: 80,
				density: {
					enable: true,
					value_area: 800
				}
			},
			color: {
				value: ['#f97316', '#fb923c', '#ff8800']
			},
			shape: {
				type: 'circle'
			},
			opacity: {
				value: 0.5,
				random: true,
				anim: {
					enable: true,
					speed: 1,
					opacity_min: 0.1,
					sync: false
				}
			},
			size: {
				value: 3,
				random: true,
				anim: {
					enable: true,
					speed: 2,
					size_min: 0.1,
					sync: false
				}
			},
			move: {
				enable: true,
				speed: 1,
				direction: 'none' as const,
				random: false,
				straight: false,
				out_mode: 'out',
				bounce: false
			}
		},
		interactivity: {
			detect_on: 'canvas',
			events: {
				onhover: {
					enable: false
				},
				onclick: {
					enable: false
				},
				resize: {
					enable: true
				}
			}
		},
		retina_detect: true
	};

	onMount(() => {
		particlesInit(async (engine) => {
			await loadSlim(engine);
		});

		// Only enable fade animations on desktop
		if (window.innerWidth >= 1024) {
			const observer = new IntersectionObserver(
				(entries) => {
					entries.forEach((entry) => {
						if (entry.target.id === 'hero-section') {
							heroVisible = entry.isIntersecting;
						} else if (entry.target.id === 'about-section') {
							aboutVisible = entry.isIntersecting;
						} else if (entry.target.id === 'abilities-section') {
							abilitiesVisible = entry.isIntersecting;
						}
					});
				},
				{ threshold: 0.5 }
			);

			const heroSection = document.getElementById('hero-section');
			const aboutSection = document.getElementById('about-section');
			const abilitiesSection = document.getElementById('abilities-section');

			if (heroSection) observer.observe(heroSection);
			if (aboutSection) observer.observe(aboutSection);
			if (abilitiesSection) observer.observe(abilitiesSection);

			return () => {
				if (heroSection) observer.unobserve(heroSection);
				if (aboutSection) observer.unobserve(aboutSection);
				if (abilitiesSection) observer.unobserve(abilitiesSection);
			};
		} else {
			// On mobile, always show sections
			heroVisible = true;
			aboutVisible = true;
			abilitiesVisible = true;
		}
	});
</script>

<div
	id="hero-section"
	class="relative hero min-h-screen overflow-hidden bg-black section-fade"
	class:visible={heroVisible}
>
	<div class="particles-container">
		<Particles id="tsparticles" options={particlesConfig} />
	</div>
	<div class="relative hero-content z-10 max-w-7xl flex-col gap-12 lg:flex-row-reverse">
		<div class="flex flex-1 items-center justify-center">
			<div class="hero-images-container">
				<div class="hero-image-wrapper hero-image-top">
					<div class="hero-glow"></div>
					<div class="hero-avatar">
						<img
							src="https://avatars.githubusercontent.com/u/119877653?v=4"
							alt="GuikiPT"
							class="avatar-img"
						/>
					</div>
				</div>
				<div class="hero-image-wrapper hero-image-bottom">
					<div class="hero-glow"></div>
					<div class="hero-avatar">
						<img
							src="https://avatars.githubusercontent.com/u/72317733?s=400&u=8afec73d662c44ad04a03653e05f73970315e7c9&v=4"
							alt="GuikiPT Discord avatar"
							class="avatar-img"
						/>
					</div>
				</div>
			</div>
		</div>
		<div class="flex-1 text-center lg:text-left">
			<h1 class="hero-title">
				Hi, I'm <span class="hero-name">GuikiPT</span>
			</h1>
			<p class="hero-aka">Also known as <span class="hero-name-alt">LuisHFF</span></p>
			<p class="hero-subtitle">Full Stack Developer</p>
			<p class="hero-description">
				I build Web, Android, and PC applications, create software for enterprise infrastructures,
				and create custom integrations that bridge software ecosystems.
			</p>
			<div class="hero-actions">
				<a href="/projects" class="btn gap-2 btn-lg btn-primary">
					View My Work
					{@html Briefcase({ size: 20 })}
				</a>
				<a href="/contact" class="hero-btn-outline btn gap-2 btn-outline btn-lg">
					Get In Touch
					{@html Mail({ size: 20 })}
				</a>
			</div>
			<!-- <div class="hero-stats">
				<div class="stat">
					<div class="stat-value text-orange-400">5+</div>
					<div class="stat-title">Years Experience</div>
				</div>
				<div class="stat">
					<div class="stat-value text-orange-400">50+</div>
					<div class="stat-title">Projects Completed</div>
				</div>
				<div class="stat">
					<div class="stat-value text-orange-400">30+</div>
					<div class="stat-title">Happy Clients</div>
				</div>
			</div> -->
		</div>
	</div>
</div>

<!-- Separator -->
<div class="separator-container">
	<div class="separator-line"></div>
	<div class="separator-glow"></div>
</div>

<!-- About Section -->
<section
	id="about-section"
	class="about-section bg-black py-20 min-h-screen flex items-center section-fade relative overflow-hidden"
	class:visible={aboutVisible}
>
	<div class="particles-container">
		<Particles id="tsparticles-about" options={particlesConfig} />
	</div>
	<div class="mx-auto max-w-7xl px-4 w-full relative z-10">
		<div class="mb-16 text-center">
			<h2 class="about-title">About Me</h2>
		</div>

		<div class="mb-16 grid items-center gap-12 lg:grid-cols-2">
			<div class="about-content">
				<!-- <h3 class="about-heading">Who I Am</h3> -->
				<p class="about-text">
					I'm <span class="hero-name-alt">Luis Henrique Ferreira de Freitas</span>, a
					<span class="hero-name-alt">22-year-old</span>
					full-stack developer from Algarve, <span class="portugal-flag">Portugal</span>.
					<br />
					I go online by <span class="hero-name-alt">GuikiPT</span> or
					<span class="hero-name-alt">LuisHFF</span>.
				</p>
				<p class="about-text">
					I work with Odoo development and administration, using Python and XML I do focus on
					customizing modules, designing procurement and custom business workflows, as well as
					writing SQL queries for complex data handling and database migrations.
				</p>
				<p class="about-text">
					Beyond Odoo, I develop Web, Mobile and Desktop applications using Node.js, Flutter, and
					Python, and manage Linux server environments, including Docker-based infrastructure for
					scalable deployments. I specialize in custom integrations, workflow automation, and
					building API bridges that connect diverse software ecosystems.
				</p>
				<p class="about-text">
					In my free time, I build hobby projects such as Discord bot integrations, APIs, and gaming
					tools, manage custom VPS hosting environments, listen to music, play games, and spend time
					learning through courses and research.
				</p>
			</div>

			<div class="about-cards">
				<div class="about-card">
					<div class="card-icon">
					{@html Code({ size: 32 })}
					</div>
					<h4 class="card-title">Full-Stack Development</h4>
					<p class="card-text">
						Building web, mobile, and desktop applications using Node.js, Flutter, and Python.
					</p>
				</div>
				<div class="about-card">
					<div class="card-icon">
					{@html Rocket({ size: 32 })}
					</div>
					<h4 class="card-title">Infrastructure</h4>
					<p class="card-text">
						Managing Linux servers, Docker containers, and VPS environments for scalable
						infrastructure.
					</p>
				</div>
				<div class="about-card">
					<div class="card-icon">
					{@html Briefcase({ size: 32 })}
					</div>
					<h4 class="card-title">Enterprise Solutions</h4>
					<p class="card-text">
						Building and customizing Odoo ERP modules for complex business workflows and enterprise
						operations.
					</p>
				</div>
				<div class="about-card">
					<div class="card-icon">
					{@html Lightbulb({ size: 32 })}
					</div>
					<h4 class="card-title">System Integration</h4>
					<p class="card-text">
						Connecting software through APIs, automation tools, and custom bridges.
					</p>
				</div>
			</div>
		</div>
	</div>
</section>

<!-- Separator -->
<div class="separator-container">
	<div class="separator-line"></div>
	<div class="separator-glow"></div>
</div>

<!-- Abilities Section -->
<section
	id="abilities-section"
	class="abilities-section bg-black py-20 min-h-screen flex items-center section-fade relative overflow-hidden"
	class:visible={abilitiesVisible}
>
	<div class="particles-container">
		<Particles id="tsparticles-abilities" options={particlesConfig} />
	</div>
	<div class="mx-auto max-w-7xl px-4 w-full relative z-10">
		<div class="mb-16 text-center">
			<h2 class="abilities-title">Technical Abilities</h2>
			<p class="abilities-subtitle">Technologies I work with</p>
		</div>

		<div class="abilities-grid">
			<!-- JavaScript/Web Stack -->
			<div class="ability-card">
				<div class="ability-icons-group">
					<div class="ability-icon-wrapper">
						<svg
							class="ability-icon"
							viewBox="0 0 256 289"
							xmlns="http://www.w3.org/2000/svg"
							preserveAspectRatio="xMidYMid"
						>
							<path
								d="M127.999 288.463c-3.975 0-7.685-1.06-11.13-2.915l-35.247-20.936c-5.3-2.915-2.65-3.975-1.06-4.505 7.155-2.385 8.48-2.915 15.9-7.156.796-.53 1.856-.265 2.65.265l27.032 16.166c1.06.53 2.385.53 3.18 0l105.74-61.217c1.06-.53 1.59-1.59 1.59-2.915V83.08c0-1.325-.53-2.385-1.59-2.915l-105.74-60.953c-1.06-.53-2.385-.53-3.18 0L20.405 80.166c-1.06.53-1.59 1.855-1.59 2.915v122.17c0 1.06.53 2.385 1.59 2.915l28.887 16.695c15.636 7.95 25.44-1.325 25.44-10.6V93.68c0-1.59 1.326-3.18 3.181-3.18h13.516c1.59 0 3.18 1.325 3.18 3.18v120.58c0 20.936-11.396 33.126-31.272 33.126-6.095 0-10.865 0-24.38-6.625l-27.827-15.9C4.24 220.885 0 213.465 0 205.515V83.346C0 75.396 4.24 67.976 11.13 64L116.87 2.783c6.625-3.71 15.635-3.71 22.26 0L244.87 64C251.76 67.975 256 75.395 256 83.346v122.17c0 7.95-4.24 15.37-11.13 19.345L139.13 286.078c-3.445 1.59-7.42 2.385-11.13 2.385zm32.596-84.009c-46.377 0-55.917-21.2-55.917-39.221 0-1.59 1.325-3.18 3.18-3.18h13.78c1.59 0 2.916 1.06 2.916 2.65 2.12 14.045 8.215 20.936 36.306 20.936 22.261 0 31.802-5.035 31.802-16.96 0-6.891-2.65-11.926-37.367-15.372-28.886-2.915-46.907-9.275-46.907-32.33 0-21.467 18.021-34.186 48.232-34.186 33.921 0 50.617 11.66 52.737 37.101 0 .795-.265 1.59-.795 2.385-.53.53-1.325 1.06-2.12 1.06h-13.78c-1.326 0-2.651-1.06-2.916-2.385-3.18-14.575-11.395-19.345-33.126-19.345-24.38 0-27.296 8.48-27.296 14.84 0 7.686 3.445 10.07 36.306 14.31 32.597 4.24 47.967 10.335 47.967 33.39-.265 23.32-19.345 36.571-53.002 36.571z"
								fill="#339933"
							/>
						</svg>
					</div>
					<div class="ability-icon-wrapper">
						<svg
							class="ability-icon"
							viewBox="0 0 256 228"
							xmlns="http://www.w3.org/2000/svg"
							preserveAspectRatio="xMidYMid"
						>
							<path
								d="M210.483 73.824a171.49 171.49 0 0 0-8.24-2.597c.465-1.9.893-3.777 1.273-5.621 6.238-30.281 2.16-54.676-11.769-62.708-13.355-7.7-35.196.329-57.254 19.526a171.23 171.23 0 0 0-6.375 5.848 155.866 155.866 0 0 0-4.241-3.917C100.759 3.829 77.587-4.822 63.673 3.233 50.33 10.957 46.379 33.89 51.995 62.588a170.974 170.974 0 0 0 1.892 8.48c-3.28.932-6.445 1.924-9.474 2.98C17.309 83.498 0 98.307 0 113.668c0 15.865 18.582 31.778 46.812 41.427a145.52 145.52 0 0 0 6.921 2.165 167.467 167.467 0 0 0-2.01 9.138c-5.354 28.2-1.173 50.591 12.134 58.266 13.744 7.926 36.812-.22 59.273-19.855a145.567 145.567 0 0 0 5.342-4.923 168.064 168.064 0 0 0 6.92 6.314c21.758 18.722 43.246 26.282 56.54 18.586 13.731-7.949 18.194-32.003 12.4-61.268a145.016 145.016 0 0 0-1.535-6.842c1.62-.48 3.21-.974 4.76-1.488 29.348-9.723 48.443-25.443 48.443-41.52 0-15.417-17.868-30.326-45.517-39.844Zm-6.365 70.984c-1.4.463-2.836.91-4.3 1.345-3.24-10.257-7.612-21.163-12.963-32.432 5.106-11 9.31-21.767 12.459-31.957 2.619.758 5.16 1.557 7.61 2.4 23.69 8.156 38.14 20.213 38.14 29.504 0 9.896-15.606 22.743-40.946 31.14Zm-10.514 20.834c2.562 12.94 2.927 24.64 1.23 33.787-1.524 8.219-4.59 13.698-8.382 15.893-8.067 4.67-25.32-1.4-43.927-17.412a156.726 156.726 0 0 1-6.437-5.87c7.214-7.889 14.423-17.06 21.459-27.246 12.376-1.098 24.068-2.894 34.671-5.345.522 2.107.986 4.173 1.386 6.193ZM87.276 214.515c-7.882 2.783-14.16 2.863-17.955.675-8.075-4.657-11.432-22.636-6.853-46.752a156.923 156.923 0 0 1 1.869-8.499c10.486 2.32 22.093 3.988 34.498 4.994 7.084 9.967 14.501 19.128 21.976 27.15a134.668 134.668 0 0 1-4.877 4.492c-9.933 8.682-19.886 14.842-28.658 17.94ZM50.35 144.747c-12.483-4.267-22.792-9.812-29.858-15.863-6.35-5.437-9.555-10.836-9.555-15.216 0-9.322 13.897-21.212 37.076-29.293 2.813-.98 5.757-1.905 8.812-2.773 3.204 10.42 7.406 21.315 12.477 32.332-5.137 11.18-9.399 22.249-12.634 32.792a134.718 134.718 0 0 1-6.318-1.979Zm12.378-84.26c-4.811-24.587-1.616-43.134 6.425-47.789 8.564-4.958 27.502 2.111 47.463 19.835a144.318 144.318 0 0 1 3.841 3.545c-7.438 7.987-14.787 17.08-21.808 26.988-12.04 1.116-23.565 2.908-34.161 5.309a160.342 160.342 0 0 1-1.76-7.887Zm110.427 27.268a347.8 347.8 0 0 0-7.785-12.803c8.168 1.033 15.994 2.404 23.343 4.08-2.206 7.072-4.956 14.465-8.193 22.045a381.151 381.151 0 0 0-7.365-13.322Zm-45.032-43.861c5.044 5.465 10.096 11.566 15.065 18.186a322.04 322.04 0 0 0-30.257-.006c4.974-6.559 10.069-12.652 15.192-18.18ZM82.802 87.83a323.167 323.167 0 0 0-7.227 13.238c-3.184-7.553-5.909-14.98-8.134-22.152 7.304-1.634 15.093-2.97 23.209-3.984a321.524 321.524 0 0 0-7.848 12.897Zm8.081 65.352c-8.385-.936-16.291-2.203-23.593-3.793 2.26-7.3 5.045-14.885 8.298-22.6a321.187 321.187 0 0 0 7.257 13.246c2.594 4.48 5.28 8.868 8.038 13.147Zm37.542 31.03c-5.184-5.592-10.354-11.779-15.403-18.433 4.902.192 9.899.29 14.978.29 5.218 0 10.376-.117 15.453-.343-4.985 6.774-10.018 12.97-15.028 18.486Zm52.198-57.817c3.422 7.8 6.306 15.345 8.596 22.52-7.422 1.694-15.436 3.058-23.88 4.071a382.417 382.417 0 0 0 7.859-13.026 347.403 347.403 0 0 0 7.425-13.565Zm-16.898 8.101a358.557 358.557 0 0 1-12.281 19.815 329.4 329.4 0 0 1-23.444.823c-7.967 0-15.716-.248-23.178-.732a310.202 310.202 0 0 1-12.513-19.846h.001a307.41 307.41 0 0 1-10.923-20.627 310.278 310.278 0 0 1 10.89-20.637l-.001.001a307.318 307.318 0 0 1 12.413-19.761c7.613-.576 15.42-.876 23.31-.876H128c7.926 0 15.743.303 23.354.883a329.357 329.357 0 0 1 12.335 19.695 358.489 358.489 0 0 1 11.036 20.54 329.472 329.472 0 0 1-11 20.722Zm22.56-122.124c8.572 4.944 11.906 24.881 6.52 51.026-.344 1.668-.73 3.367-1.15 5.09-10.622-2.452-22.155-4.275-34.23-5.408-7.034-10.017-14.323-19.124-21.64-27.008a160.789 160.789 0 0 1 5.888-5.4c18.9-16.447 36.564-22.941 44.612-18.3ZM128 90.808c12.625 0 22.86 10.235 22.86 22.86s-10.235 22.86-22.86 22.86-22.86-10.235-22.86-22.86 10.235-22.86 22.86-22.86Z"
								fill="#61DAFB"
							/>
						</svg>
					</div>
					<div class="ability-icon-wrapper">
						<svg
							class="ability-icon"
							viewBox="0 0 98.1 118"
							xmlns="http://www.w3.org/2000/svg"
							preserveAspectRatio="xMidYMid"
						>
							<path
								d="M91.8 15.6C80.9-.1 59.2-4.7 43.6 5.2L16.1 22.8C8.6 27.5 3.4 35.2 1.9 43.9c-1.3 7.3-.2 14.8 3.3 21.3-2.4 3.6-4 7.6-4.7 11.8-1.6 8.9.5 18.1 5.7 25.4 11 15.7 32.6 20.3 48.2 10.4l27.5-17.5c7.5-4.7 12.7-12.4 14.2-21.1 1.3-7.3.2-14.8-3.3-21.3 2.4-3.6 4-7.6 4.7-11.8 1.6-8.9-.5-18.1-5.7-25.4z"
								fill="#FF3E00"
							/>
							<path
								d="M40.9 103.9c-8.9 2.3-18.2-1.2-23.4-8.7-3.2-4.4-4.4-9.9-3.5-15.3.2-.9.4-1.7.6-2.6l.5-1.6 1.4 1c3.3 2.4 6.9 4.2 10.8 5.4l1 .3-.1 1c-.1 1.4.3 2.9 1.1 4.1 1.6 2.3 4.4 3.4 7.1 2.7.6-.2 1.2-.4 1.7-.7L65.5 72c1.4-.9 2.3-2.2 2.6-3.8.3-1.6-.1-3.3-1-4.6-1.6-2.3-4.4-3.3-7.1-2.6-.6.2-1.2.4-1.7.7l-10.5 6.7c-1.7 1.1-3.6 1.9-5.6 2.4-8.9 2.3-18.2-1.2-23.4-8.7-3.1-4.4-4.4-9.9-3.4-15.3.9-5.2 4.1-9.9 8.6-12.7l27.5-17.5c1.7-1.1 3.6-1.9 5.6-2.5 8.9-2.3 18.2 1.2 23.4 8.7 3.2 4.4 4.4 9.9 3.5 15.3-.2.9-.4 1.7-.7 2.6l-.5 1.6-1.4-1c-3.3-2.4-6.9-4.2-10.8-5.4l-1-.3.1-1c.1-1.4-.3-2.9-1.1-4.1-1.6-2.3-4.4-3.3-7.1-2.6-.6.2-1.2.4-1.7.7L32.4 46.1c-1.4.9-2.3 2.2-2.6 3.8s.1 3.3 1 4.6c1.6 2.3 4.4 3.3 7.1 2.6.6-.2 1.2-.4 1.7-.7l10.5-6.7c1.7-1.1 3.6-1.9 5.6-2.5 8.9-2.3 18.2 1.2 23.4 8.7 3.2 4.4 4.4 9.9 3.5 15.3-.9 5.2-4.1 9.9-8.6 12.7l-27.5 17.5c-1.7 1.1-3.6 1.9-5.6 2.5z"
								fill="#FFF"
							/>
						</svg>
					</div>
				</div>
				<h3 class="ability-name">Node.js + React + Svelte</h3>
				<p class="ability-description">
					Full-stack JavaScript/TypeScript development with modern frameworks and server-side
					capabilities.
				</p>
			</div>

			<!-- Flutter & Dart -->
			<div class="ability-card">
				<div class="ability-icons-group">
					<div class="ability-icon-wrapper">
						<svg
							class="ability-icon"
							viewBox="0 0 256 317"
							xmlns="http://www.w3.org/2000/svg"
							preserveAspectRatio="xMidYMid"
						>
							<defs>
								<linearGradient id="flutter-gradient" x1="3.952%" y1="26.993%" x2="75.897%" y2="52.919%">
									<stop offset="0%" stop-color="#47C5FB" />
									<stop offset="100%" stop-color="#02569B" />
								</linearGradient>
							</defs>
							<path
								d="M157.665 0 0 157.665 48.526 206.19 255.991 0H157.665Z"
								fill="#47C5FB"
							/>
							<path d="M156.567 145.396 72.09 229.873l48.526 48.527 145.49-145.49h-109.54Z" fill="#02569B" />
							<path
								d="m121.132 279.502 47.015-47.015 48.525 48.526-47.015 47.015z"
								fill="url(#flutter-gradient)"
							/>
						</svg>
					</div>
					<div class="ability-icon-wrapper">
						<svg
							class="ability-icon"
							viewBox="0 0 1080 1080"
							xmlns="http://www.w3.org/2000/svg"
							preserveAspectRatio="xMidYMid"
						>
							<path fill="#01579B" d="M225.6,852.14L44.84,671.38c-21.41-22.01-34.76-53.08-34.76-83.43c0-14.05,7.94-36.03,13.9-48.67l166.86-347.62L225.6,852.14z"/>
							<path fill="#40C4FF" d="M844.37,226.42L663.61,45.66c-15.79-15.85-48.67-34.76-76.48-34.76c-23.9,0-47.36,4.78-62.57,13.9L190.84,191.66L844.37,226.42z"/>
							<polygon fill="#40C4FF" points="441.13,1067.66 879.13,1067.66 879.13,879.95 552.37,775.66 253.41,879.95"/>
							<path fill="#29B6F6" d="M190.84,754.8c0,55.77,6.99,69.45,34.76,97.33l27.81,27.81h625.72L573.22,532.33L190.84,191.66V754.8z"/>
							<path fill="#01579B" d="M747.03,191.66H190.84l688.29,688.29h187.71V448.9L844.37,226.42C813.12,195.05,785.37,191.66,747.03,191.66z"/>
						</svg>
					</div>
				</div>
		<h3 class="ability-name">Flutter + Dart</h3>
		<p class="ability-description">
			Cross-platform mobile development for iOS and Android with beautiful, native interfaces.
		</p>
	</div>

			<!-- Python -->
			<div class="ability-card">
				<div class="ability-icons-group">
					<div class="ability-icon-wrapper">
						<svg
							class="ability-icon"
							viewBox="0 0 256 255"
							xmlns="http://www.w3.org/2000/svg"
							preserveAspectRatio="xMidYMid"
						>
							<defs>
								<linearGradient id="python-gradient-1" x1="12.959%" y1="12.039%" x2="79.639%" y2="78.201%">
									<stop offset="0%" stop-color="#387EB8" />
									<stop offset="100%" stop-color="#366994" />
								</linearGradient>
								<linearGradient id="python-gradient-2" x1="19.128%" y1="20.579%" x2="90.742%" y2="88.429%">
									<stop offset="0%" stop-color="#FFE873" />
									<stop offset="100%" stop-color="#FFC331" />
								</linearGradient>
							</defs>
							<path
								d="M126.916.072c-64.832 0-60.784 28.115-60.784 28.115l.072 29.128h61.868v8.745H41.631S.145 61.355.145 126.77c0 65.417 36.21 63.097 36.21 63.097h21.61v-30.356s-1.165-36.21 35.632-36.21h61.362s34.475.557 34.475-33.319V33.97S194.67.072 126.916.072ZM92.802 19.66a11.12 11.12 0 0 1 11.13 11.13 11.12 11.12 0 0 1-11.13 11.13 11.12 11.12 0 0 1-11.13-11.13 11.12 11.12 0 0 1 11.13-11.13Z"
								fill="url(#python-gradient-1)"
							/>
							<path
								d="M128.757 254.126c64.832 0 60.784-28.115 60.784-28.115l-.072-29.127H127.6v-8.745h86.441s41.486 4.705 41.486-60.712c0-65.416-36.21-63.096-36.21-63.096h-21.61v30.355s1.165 36.21-35.632 36.21h-61.362s-34.475-.557-34.475 33.32v56.013s-5.235 33.897 62.518 33.897Zm34.114-19.586a11.12 11.12 0 0 1-11.13-11.13 11.12 11.12 0 0 1 11.13-11.131 11.12 11.12 0 0 1 11.13 11.13 11.12 11.12 0 0 1-11.13 11.13Z"
								fill="url(#python-gradient-2)"
							/>
						</svg>
					</div>
					<div class="ability-icon-wrapper">
						<svg
							class="ability-icon"
							viewBox="0 0 36 24"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							stroke="#fb923c"
							stroke-width="2"
							stroke-linecap="round"
							stroke-linejoin="round"
						>
							<polyline points="10 6 4 12 10 18"/>
							<line x1="19" y1="5" x2="17" y2="19"/>
							<polyline points="26 18 32 12 26 6"/>
						</svg>
					</div>
				</div>
				<h3 class="ability-name">Python + XML</h3>
				<p class="ability-description">
					Backend development, automation, Odoo ERP modules with XML views, and scripting.
				</p>
			</div>

			<!-- Bash -->
			<div class="ability-card">
				<div class="ability-icons-group">
					<div class="ability-icon-wrapper">
						<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4b/Bash_Logo_Colored.svg/960px-Bash_Logo_Colored.svg.png" alt="Bash Logo" class="ability-icon" />
					</div>
					<div class="ability-icon-wrapper">
						<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Tux.svg/1200px-Tux.svg.png" alt="Linux Logo" class="ability-icon" />
					</div>
				</div>
				<h3 class="ability-name">Bash + Linux</h3>
				<p class="ability-description">
					Shell scripting, automation, system administration, and Linux server management.
				</p>
			</div>

			<!-- Databases -->
			<div class="ability-card">
				<div class="ability-icons-group">
					<div class="ability-icon-wrapper">
						<img src="https://www.svgrepo.com/show/354037/mariadb-icon.svg" alt="MariaDB Logo" class="ability-icon" />
					</div>
					<div class="ability-icon-wrapper">
						<img src="https://www.postgresql.org/media/img/about/press/elephant.png" alt="PostgreSQL Logo" class="ability-icon" />
					</div>
					<div class="ability-icon-wrapper">
						<img src="https://raw.githubusercontent.com/gilbarbara/logos/main/logos/supabase-icon.svg" alt="Supabase Logo" class="ability-icon" />
					</div>
				</div>
				<h3 class="ability-name">MariaDB + PostgreSQL + Supabase</h3>
				<p class="ability-description">
					Relational database management, SQL optimization, and modern backend-as-a-service platforms.
				</p>
			</div>
		</div>
	</div>
</section>

<style>
	/* Fade animations only on desktop */
	@media (min-width: 1024px) {
		.section-fade {
			opacity: 0;
			transform: translateY(20px);
			transition:
				opacity 1s cubic-bezier(0.4, 0, 0.2, 1),
				transform 1s cubic-bezier(0.4, 0, 0.2, 1);
		}

		.section-fade.visible {
			opacity: 1;
			transform: translateY(0);
		}
	}

	/* On mobile, sections are always visible */
	@media (max-width: 1023px) {
		.section-fade {
			opacity: 1;
			transform: translateY(0);
		}
	}

	.particles-container {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: 1;
		transition: opacity 0.8s ease-out;
	}

	@media (min-width: 1024px) {
		.section-fade:not(.visible) .particles-container {
			opacity: 0;
		}
	}

	.hero-title {
		font-size: 3rem;
		font-weight: 800;
		line-height: 1.2;
		margin-bottom: 1rem;
		color: #fff;
	}

	.hero-name {
		font-family: 'Bungee Shade', sans-serif;
		color: #fb923c;
		text-shadow:
			0 0 15px rgba(249, 115, 22, 0.7),
			0 0 30px rgba(249, 115, 22, 0.5);
		display: inline-block;
	}

	.hero-aka {
		font-size: 0.875rem;
		color: #6b7280;
		margin-bottom: 0.75rem;
		font-style: italic;
	}

	.hero-name-alt {
		font-weight: 600;
		color: #fb923c;
		text-shadow:
			0 0 8px rgba(249, 115, 22, 0.5),
			0 0 15px rgba(249, 115, 22, 0.3);
		display: inline-block;
		font-style: normal;
	}

	.portugal-flag {
		font-weight: 600;
		background: linear-gradient(90deg, #006600 0%, #006600 40%, #ff0000 60%, #ff0000 100%);
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		background-clip: text;
		text-shadow:
			0 0 8px rgba(0, 102, 0, 0.5),
			0 0 15px rgba(255, 0, 0, 0.3);
		display: inline-block;
		font-style: normal;
		filter: drop-shadow(0 0 8px rgba(0, 102, 0, 0.4)) drop-shadow(0 0 12px rgba(255, 0, 0, 0.3));
	}

	.hero-subtitle {
		font-size: 1.5rem;
		font-weight: 600;
		color: #fb923c;
		margin-bottom: 1rem;
	}

	.hero-description {
		font-size: 1.125rem;
		color: #9ca3af;
		margin-bottom: 2rem;
		line-height: 1.75;
	}

	.hero-actions {
		display: flex;
		gap: 1rem;
		margin-bottom: 3rem;
		flex-wrap: wrap;
	}

	.hero-btn-outline {
		border-color: #f97316;
		color: #fb923c;
	}

	.hero-btn-outline:hover {
		background: rgba(249, 115, 22, 0.1);
		border-color: #fb923c;
		color: #fff7ed;
		box-shadow:
			0 0 15px rgba(249, 115, 22, 0.6),
			0 0 30px rgba(249, 115, 22, 0.4);
	}

	/* .hero-stats {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		gap: 1rem;
		margin-top: 2rem;
	}

	.stat {
		text-align: center;
		padding: 1rem;
		background: rgba(249, 115, 22, 0.05);
		border-radius: 0.75rem;
		border: 1px solid rgba(249, 115, 22, 0.2);
		transition: all 200ms ease;
	}

	.stat:hover {
		background: rgba(249, 115, 22, 0.1);
		border-color: rgba(249, 115, 22, 0.4);
		transform: translateY(-4px);
		box-shadow:
			0 0 20px rgba(249, 115, 22, 0.3),
			0 0 40px rgba(249, 115, 22, 0.2);
	}

	.stat-value {
		font-size: 2.5rem;
		font-weight: 800;
	}

	.stat-title {
		font-size: 0.875rem;
		color: #9ca3af;
		text-transform: uppercase;
		letter-spacing: 0.05em;
	} */

	.hero-images-container {
		position: relative;
		width: 100%;
		max-width: 550px;
		height: 550px;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.hero-image-wrapper {
		position: absolute;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 0.5rem;
	}

	.hero-image-top {
		top: 70px;
		right: 70px;
		z-index: 2;
	}

	.hero-image-bottom {
		bottom: 70px;
		left: 70px;
		z-index: 1;
	}

	.hero-glow {
		position: absolute;
		width: 100%;
		height: 100%;
		background: radial-gradient(circle, rgba(249, 115, 22, 0.3) 0%, transparent 70%);
		border-radius: 50%;
		animation: pulse-glow 3s ease-in-out infinite;
		top: 0;
		left: 0;
	}

	.hero-avatar {
		position: relative;
		width: 250px;
		height: 250px;
		border-radius: 50%;
		border: 4px solid #f97316;
		background: linear-gradient(135deg, rgba(249, 115, 22, 0.1) 0%, rgba(0, 0, 0, 0.8) 100%);
		box-shadow:
			0 0 40px rgba(249, 115, 22, 0.6),
			0 0 80px rgba(249, 115, 22, 0.4),
			inset 0 0 60px rgba(249, 115, 22, 0.1);
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: center;
	}

	.avatar-img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		border-radius: 50%;
	}

	@keyframes pulse-glow {
		0%,
		100% {
			transform: scale(1);
			opacity: 0.6;
		}
		50% {
			transform: scale(1.1);
			opacity: 0.8;
		}
	}

	@media (max-width: 1024px) {
		.hero-title {
			font-size: 2.5rem;
		}

		.hero-subtitle {
			font-size: 1.25rem;
		}

		.hero-actions {
			justify-content: center;
		}
		/* 
		.hero-stats {
			grid-template-columns: 1fr;
		} */

		.hero-images-container {
			width: 280px;
			height: 280px;
		}

		.hero-avatar {
			width: 140px;
			height: 140px;
		}

		.hero-image-top {
			top: 30px;
			right: 30px;
		}

		.hero-image-bottom {
			bottom: 30px;
			left: 30px;
		}
	}

	/* Separator Styles */
	.separator-container {
		position: relative;
		width: 100%;
		height: 2px;
		background: black;
		overflow: hidden;
	}

	.separator-line {
		position: absolute;
		width: 100%;
		height: 100%;
		background: linear-gradient(90deg, transparent 0%, #f97316 50%, transparent 100%);
	}

	.separator-glow {
		position: absolute;
		width: 100%;
		height: 40px;
		top: -19px;
		background: radial-gradient(ellipse at center, rgba(249, 115, 22, 0.4) 0%, transparent 70%);
	}

	/* About Section Styles */
	.about-title {
		font-family: 'Bungee Shade', sans-serif;
		font-size: 3rem;
		color: #fb923c;
		text-shadow:
			0 0 15px rgba(249, 115, 22, 0.7),
			0 0 30px rgba(249, 115, 22, 0.5);
		margin-bottom: 0.5rem;
	}

	.about-content {
		padding: 1rem;
	}

	/* .about-heading {
		font-size: 2rem;
		font-weight: 700;
		color: #fb923c;
		margin-bottom: 1.5rem;
		text-shadow:
			0 0 10px rgba(249, 115, 22, 0.5),
			0 0 20px rgba(249, 115, 22, 0.3);
	} */

	.about-text {
		font-size: 1.125rem;
		color: #d1d5db;
		line-height: 1.8;
		margin-bottom: 1.5rem;
	}

	.about-cards {
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		gap: 1.5rem;
	}

	.about-card {
		background: rgba(249, 115, 22, 0.05);
		border: 1px solid rgba(249, 115, 22, 0.2);
		border-radius: 1rem;
		padding: 2rem;
		transition: all 300ms ease;
		text-align: center;
	}

	.about-card:hover {
		background: rgba(249, 115, 22, 0.1);
		border-color: rgba(249, 115, 22, 0.4);
		transform: translateY(-8px);
		box-shadow:
			0 0 30px rgba(249, 115, 22, 0.4),
			0 0 60px rgba(249, 115, 22, 0.2);
	}

	.card-icon {
		display: inline-flex;
		align-items: center;
		justify-content: center;
		width: 64px;
		height: 64px;
		border-radius: 50%;
		background: rgba(249, 115, 22, 0.1);
		border: 2px solid #f97316;
		margin-bottom: 1rem;
		color: #fb923c;
		box-shadow:
			0 0 20px rgba(249, 115, 22, 0.3),
			inset 0 0 20px rgba(249, 115, 22, 0.1);
	}

	.card-title {
		font-size: 1.25rem;
		font-weight: 700;
		color: #fb923c;
		margin-bottom: 0.75rem;
		text-align: center;
		width: 100%;
		display: block;
	}

	.card-text {
		font-size: 0.95rem;
		color: #9ca3af;
		line-height: 1.6;
		text-align: center;
	}

	@media (max-width: 1024px) {
		.about-title {
			font-size: 2rem;
		}

		/* .about-heading {
			font-size: 1.5rem;
		} */

		.about-cards {
			grid-template-columns: 1fr;
		}
	}

	/* Abilities Section Styles */
	.abilities-title {
		font-family: 'Bungee Shade', sans-serif;
		font-size: 3rem;
		color: #fb923c;
		text-shadow:
			0 0 15px rgba(249, 115, 22, 0.7),
			0 0 30px rgba(249, 115, 22, 0.5);
		margin-bottom: 0.5rem;
	}

	.abilities-subtitle {
		font-size: 1.125rem;
		color: #9ca3af;
		margin-top: 0.5rem;
	}

	.abilities-grid {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
		gap: 2rem;
		max-width: 1200px;
		margin: 0 auto;
	}

	@media (min-width: 900px) {
		.abilities-grid {
			grid-template-columns: repeat(6, 1fr);
		}

		.ability-card {
			grid-column: span 2;
		}

		.ability-card:nth-child(4) {
			grid-column: 2 / 4;
		}

		.ability-card:nth-child(5) {
			grid-column: 4 / 6;
		}
	}

	.ability-card {
		background: rgba(249, 115, 22, 0.05);
		border: 1px solid rgba(249, 115, 22, 0.2);
		border-radius: 1rem;
		padding: 2rem;
		transition: all 300ms ease;
		display: flex;
		flex-direction: column;
		align-items: center;
		text-align: center;
	}

	.ability-card:hover {
		background: rgba(249, 115, 22, 0.1);
		border-color: rgba(249, 115, 22, 0.4);
		transform: translateY(-8px) scale(1.02);
		box-shadow:
			0 0 30px rgba(249, 115, 22, 0.4),
			0 0 60px rgba(249, 115, 22, 0.2);
	}

	.ability-icon-wrapper {
		width: 80px;
		height: 80px;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 50%;
		background: rgba(249, 115, 22, 0.1);
		border: 2px solid #f97316;
		padding: 1rem;
		box-shadow:
			0 0 20px rgba(249, 115, 22, 0.3),
			inset 0 0 20px rgba(249, 115, 22, 0.1);
		transition: all 300ms ease;
	}

	.ability-icons-group {
		display: flex;
		gap: 1rem;
		margin-bottom: 1.5rem;
		flex-wrap: wrap;
		justify-content: center;
	}

	.ability-icons-group .ability-icon-wrapper {
		margin-bottom: 0;
	}

	.ability-card:hover .ability-icon-wrapper {
		transform: scale(1.1);
		box-shadow:
			0 0 30px rgba(249, 115, 22, 0.5),
			inset 0 0 30px rgba(249, 115, 22, 0.2);
	}

	.ability-icon {
		width: 100%;
		height: 100%;
	}

	.ability-name {
		font-size: 1.5rem;
		font-weight: 700;
		color: #fb923c;
		margin-bottom: 1rem;
		text-shadow:
			0 0 10px rgba(249, 115, 22, 0.4),
			0 0 20px rgba(249, 115, 22, 0.2);
	}

	.ability-description {
		font-size: 1rem;
		color: #9ca3af;
		line-height: 1.6;
	}

	@media (max-width: 1024px) {
		.abilities-title {
			font-size: 2rem;
		}

		.abilities-grid {
			grid-template-columns: 1fr;
			gap: 1.5rem;
		}
	}
</style>
