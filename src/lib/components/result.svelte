<script lang="ts">
	interface Props {
		result: 'win' | 'lose' | 'tie';
		playAgain: () => void;
	}

	let { result, playAgain }: Props = $props();

	let resultMessage = $derived(
		{
			win: 'YOU WIN',
			lose: 'YOU LOSE',
			tie: "IT'S A TIE"
		}[result]
	);
</script>

<div class="flex flex-col items-center gap-y-4">
	<h2 class="text-[56px] leading-tight font-bold whitespace-nowrap text-white">
		{resultMessage}
	</h2>
	<button
		class="rounded-lg bg-white px-16 py-4 leading-tight font-semibold tracking-[2.5px] text-navy-900"
		onclick={playAgain}
		>PLAY AGAIN
	</button>
</div>
