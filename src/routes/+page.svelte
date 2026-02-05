<script lang="ts">
	import { onMount } from 'svelte';
	import Footer from './footer/footer.svelte';

	let PlatformInformation = $state<string>('');
	let LanguageInformation = $state<string>('');
	let VersionInformation = $state<string>('');
	let NameInformation = $state<string>('');
	let ScreenResolutionInformation = $state<string>('');
	let ScreenWidthInformation = $state<number>(0);
	let ScreenHeightInformation = $state<number>(0);
	let NetworkStatusInformation = $state<string>('');
	let TimezoneInformation = $state<string>('');
	let LocalTimeInformation = $state<string>('');

	const GenerateInformation = () => {
		PlatformInformation = navigator.userAgentData?.platform || 'unknown';
		LanguageInformation = navigator.language;
		VersionInformation = navigator.userAgent;
		NameInformation = navigator.appName;
		ScreenResolutionInformation = `${window.screen.width} x ${window.screen.height}`;
		ScreenWidthInformation = window.innerWidth;
		ScreenHeightInformation = window.innerHeight;
		NetworkStatusInformation = navigator.onLine ? 'Online' : 'Offline';

		window.addEventListener('online', () => {
			NetworkStatusInformation = 'Online';
		});
		window.addEventListener('offline', () => {
			NetworkStatusInformation = 'Offline';
		});

		TimezoneInformation = Intl.DateTimeFormat().resolvedOptions().timeZone;
		LocalTimeInformation = new Date().toLocaleString();
	};

	const ClearInformation = () => {
		PlatformInformation = '';
		LanguageInformation = '';
		VersionInformation = '';
		NameInformation = '';
		ScreenResolutionInformation = '';
		ScreenWidthInformation = 0;
		ScreenHeightInformation = 0;
		NetworkStatusInformation = '';
		TimezoneInformation = '';
		LocalTimeInformation = '';
	};
</script>

<section class="bg-gray-100 min-h-screen flex flex-col gap-5 relative">
	<h1 class="text-2xl font-bold text-center py-6 text-gray-200 bg-gray-700">
		(System Information Project)
	</h1>
	<div
		class="border p-5 flex flex-col gap-5 rounded-md shadow-lg sm:max-w-200 sm:w-100 max-w-200 relative w-80 mr-auto ml-auto"
	>
		<h1 class="font-bold text-center font-sans text-2xl">System Information Report</h1>
		<div class="flex flex-col gap-3">
			<span class="flex gap-1"
				>Platform: <span class="border-b border-black">{PlatformInformation}</span>
			</span>
			<span class="flex gap-1"
				>Language: <span class="border-b border-black">{LanguageInformation}</span>
			</span>
			<span class="flex gap-1"
				>Version: <span class="border-b border-black">{VersionInformation}</span>
			</span>
			<span class="flex gap-1"
				>Name: <span class="border-b border-black">{NameInformation}</span>
			</span>
			<span
				>Screen Resolution: <span class="border-b border-black">{ScreenResolutionInformation}</span>
			</span>
			<span
				>Screen Width: <span class="border-b border-black">{ScreenWidthInformation}</span>
			</span>
			<span
				>Screen Height: <span class="border-b border-black">{ScreenHeightInformation}</span>
			</span>
			<span
				>Network Status: <span class="border-b border-black">{NetworkStatusInformation}</span></span
			>
			<span>Time Zone: <span class="border-b border-black">{TimezoneInformation}</span></span>
			<span>Local Time: <span class="border-b border-black">{LocalTimeInformation}</span></span>
		</div>

		<div class="flex flex-col gap-2">
			<button
				class="bg-blue-700 active:scale-95 cursor-pointer text-white hover:bg-blue-600 rounded-sm py-1"
				onclick={GenerateInformation}>Generate</button
			>
			<button
				class="bg-gray-700 text-gray-200 active:scale-95 cursor-pointer hover:bg-gray-900 rounded-sm py-1"
				onclick={ClearInformation}>Clear</button
			>
		</div>
	</div>
</section>
<Footer></Footer>
