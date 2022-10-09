<script lang="ts" context="module">
	/**
	 * @type {import('@sveltejs/kit').Load}
	 */
	export async function load({ fetch }) {
		return {
			props: {
				blogs: await fetch(`/blog.json?recent=${3}`).then((res) => res.json()),
			},
		};
	}
</script>

<script lang="ts">
	// Start: External Imports
	// End: External Imports

	// Start: Svelte Imports
	// End: Svelte Imports

	// Start: Local Imports

	// Core services

	// Utils

	// Components
	import HeadTags from '$components/head-tags/HeadTags.svelte';
	import BlogPost from '$components/blog-post/BlogPost.svelte';
	import ProjectCard from '$components/project-card/ProjectCard.svelte';

	// Models
	import type { IMetaTagProperties } from '$models/interfaces/imeta-tag-properties.interface';
	import type { IProjectCard } from '$models/interfaces/iproject-card.interface';
	import type { IBlog } from '$models/interfaces/iblog.interface';
	// End: Local Imports

	// Exports
	export let blogs!: IBlog[];
	// Start: Local component properties
	/**
	 * @type {IMetaTagProperties}
	 */
	const metaData: Partial<IMetaTagProperties> = {
		title: `Qisthi | Personal Site`,
		description: `Hola, I'm tech enthusiast from East Java, Indonesia. Working remotely as full stack Software Engineer at Javan Cipta Solusi Company Limited.`,
		keywords: ['qisthi ramadhani', 'qisthi', 'ramadhani'],
	};

	const projects: IProjectCard[] = [
		{
			title: 'Laravolt',
			description: 'Platform untuk mengembangkan sistem informasi dalam 2 minggu',
			slug: 'https://laravolt.dev',
			icon: '',
		},
		{
			title: 'Indonesia',
			description: `Laravel package yang berisi tentang data wilayah administratif Negara Kesatuan Republik Indonesia.`,
			slug: 'https://github.com/laravolt/indonesia',
			icon: '',
		},
	];
	// End: Local component properties

	// Start: Local component methods

	// End: Local component methods
</script>

<!-- Start: Header Tag -->
<HeadTags metaData="{metaData}" />
<!-- End: Header Tag -->

<!-- Start: Home Page container -->
<div class="flex flex-col justify-center items-start max-w-2xl mx-auto mb-16">
	<h1 class="font-bold text-3xl md:text-5xl tracking-tight mb-4 text-black dark:text-white">Hey, semuanya!</h1>
	<p class="prose text-gray-600 dark:text-gray-400 mb-16">
		Nama saya Qisthi Ramadhani, seorang full stack web developer, penulis dan juga kreator di dunia maya. Saat ini
		bekerja remote dari Magetan, Jawa Timur untuk PT Javan Cipta Solusi. Lebih lanjut bisa kunjungi halaman
		<a sveltekit:prefetch href="/about" aria-label="about me" class="text-blue-700 hover:text-blue-800 transition">
			tentang saya.
		</a>
	</p>

	<!-- Start: Popular Blog Section -->
	<h2 class="font-bold text-2xl md:text-4xl tracking-tight mb-4 text-black dark:text-white">Artikel Terbaru</h2>

	{#if blogs.length > 0}
		{#each blogs as blog, index (blog.slug)}
			<BlogPost blog="{blog}" />
		{/each}
	{/if}
	<!-- End: Popular Blog Section -->

	<!-- Start: Top Projects -->
	<h2 class="font-bold text-2xl md:text-4xl tracking-tight mb-4 mt-8 text-black dark:text-white">Proyek Terbaru</h2>

	{#if projects.length > 0}
		{#each projects as project}
			<ProjectCard project="{project}" />
		{/each}
	{/if}
	<!-- End: Top Projects -->
</div>
<!-- End: Home Page container -->
