<script lang="ts">
	import {
		ArrowRight,
		Code,
		Briefcase,
		Mail,
		Lightbulb,
		Rocket,
		Users,
		Heart,
		BugIcon
	} from 'lucide-svelte';
	import Particles, { particlesInit } from '@tsparticles/svelte';
	import { loadSlim } from '@tsparticles/slim';
	import { onMount } from 'svelte';

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

	onMount(async () => {
		await particlesInit(async (engine) => {
			await loadSlim(engine);
		});
	});
</script>

<div class="relative hero min-h-screen overflow-hidden bg-black">
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
					<Briefcase size={20} />
				</a>
				<a href="/contact" class="hero-btn-outline btn gap-2 btn-outline btn-lg">
					Get In Touch
					<Mail size={20} />
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
<section class="about-section bg-black py-20">
	<div class="mx-auto max-w-7xl px-4">
		<div class="mb-16 text-center">
			<h2 class="about-title">About Me</h2>
		</div>

		<div class="mb-16 grid items-center gap-12 lg:grid-cols-2">
			<div class="about-content">
				<h3 class="about-heading">Who I Am</h3>
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
						<Code size={32} />
					</div>
					<h4 class="card-title">Full-Stack Development</h4>
					<p class="card-text">
						Building web, mobile, and desktop applications using Node.js, Flutter, and Python.
					</p>
				</div>
				<div class="about-card">
					<div class="card-icon">
						<Rocket size={32} />
					</div>
					<h4 class="card-title">Infrastructure</h4>
					<p class="card-text">
						Managing Linux servers, Docker containers, and VPS environments for scalable
						infrastructure.
					</p>
				</div>
				<div class="about-card">
					<div class="card-icon">
						<Briefcase size={32} />
					</div>
					<h4 class="card-title">Enterprise Solutions</h4>
					<p class="card-text">
						Building and customizing Odoo ERP modules for complex business workflows and enterprise
						operations.
					</p>
				</div>
				<div class="about-card">
					<div class="card-icon">
						<Lightbulb size={32} />
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

<style>
	.particles-container {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		z-index: 1;
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

	.about-subtitle {
		font-size: 1.25rem;
		color: #9ca3af;
		font-style: italic;
	}

	.about-content {
		padding: 1rem;
	}

	.about-heading {
		font-size: 2rem;
		font-weight: 700;
		color: #fb923c;
		margin-bottom: 1.5rem;
		text-shadow:
			0 0 10px rgba(249, 115, 22, 0.5),
			0 0 20px rgba(249, 115, 22, 0.3);
	}

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

		.about-heading {
			font-size: 1.5rem;
		}

		.about-cards {
			grid-template-columns: 1fr;
		}
	}
</style>
