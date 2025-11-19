<script lang="ts">
	import logo from '$lib/assets/logo.svg';
	import { m } from '$lib/paraglide/messages';

	interface Props {
		score: number;
	}

	let { score = 0 }: Props = $props();
</script>

<div
	class="flex w-full items-center justify-between rounded-sm p-3 outline-2 outline-gray-600 sm:rounded-xl sm:px-6 sm:py-4"
>
	<img src={logo} alt="Logo" class="h-15 sm:h-full" fetchpriority="high" />
	<dl class="min-w-20 rounded-sm bg-white py-2 text-center sm:min-w-38 sm:rounded-lg sm:py-4">
		<dt class="text-xs font-semibold tracking-widest text-blue-700 uppercase sm:text-base">
			{m.score()}
		</dt>
		<dd class="text-[40px] leading-none font-bold text-gray-600 sm:text-6xl">{score}</dd>
	</dl>
</div>
