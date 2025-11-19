<script lang="ts">
	import { m } from '$lib/paraglide/messages';

	interface Props {
		result: 'win' | 'lose' | 'tie';
		playAgain: () => void;
	}

	let { result, playAgain }: Props = $props();

	const resultMap = {
		win: m.you_win(),
		lose: m.you_lose(),
		tie: m.tie()
	};
	let resultMessage = $derived(resultMap[result]);
</script>

<div class="flex flex-col items-center gap-y-4">
	<h2 class="text-[56px] leading-tight font-bold whitespace-nowrap text-white uppercase">
		{resultMessage}
	</h2>
	<button
		class="rounded-lg bg-white px-16 py-4 leading-tight font-semibold tracking-[2.5px] text-navy-900 uppercase"
		onclick={playAgain}
	>
		{m.play_again()}
	</button>
</div>
