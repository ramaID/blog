<script lang="ts" context="module">
	import { browser, dev } from '$app/env';

	// we don't need any JS on this page, though we'll load
	// it in dev so that we get hot module replacement...
	export const hydrate = dev;

	// ...but if the client-side router is already loaded
	// (i.e. we came here from elsewhere in the app), use it
	export const router = browser;

	// since there's no dynamic data here, we can prerender
	// it so that it gets served as a static asset in prod
	export const prerender = true;
</script>

<script lang="ts">
	// Start: Local Imports
	// Components
	import HeadTags from '$components/head-tags/HeadTags.svelte';
	import ExternalLink from '$ui/components/external-link/ExternalLink.svelte';
	import ProjectCard from '$components/project-card/ProjectCard.svelte';

	// Models
	import type { IMetaTagProperties } from '$models/interfaces/imeta-tag-properties.interface';
	import type { IProjectCard } from '$models/interfaces/iproject-card.interface';
	// End: Local Imports

	// Start: Local component properties
	/**
	 * @type {IMetaTagProperties}
	 */
	const metaData: Partial<IMetaTagProperties> = {
		title: `Proyek Qisthi`,
		description: 'Beberapa daftar proyek open source software yang saya kerjakan, cekidot!',
		url: '/projects',
		keywords: ['proyek', 'qisthi', 'qisthi ramadhani'],
		searchUrl: '/projects',
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
</script>

<!-- Start: Header Tag -->
<HeadTags metaData="{metaData}" />
<!-- End: Header Tag -->

<!-- Start: Project page section -->
<div class="flex flex-col justify-center items-start max-w-2xl mx-auto mb-16">
	<h1 class="font-bold text-3xl md:text-5xl tracking-tight mb-4 dark:text-white">Proyek</h1>
	<div class="mb-8 prose leading-6 text-gray-600 dark:text-gray-400">
		<p>Halo, nama saya Qisthi Ramadhani. Seorang full stack web developer, penulis dan kreator di dunia maya.</p>
	</div>
	{#if projects.length > 0}
		{#each projects as project}
			<ProjectCard project="{project}" />
		{/each}
	{/if}
</div>
<!-- End: Project page section -->
