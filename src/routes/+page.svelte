<script lang="ts">
	import Header from '$lib/components/header.svelte';
	import SymbolPlaceholder from '$lib/components/symbol-placeholder.svelte';
	import Result from '$lib/components/result.svelte';
	import Symbol, { type SymbolName } from '$lib/components/symbol.svelte';
	import { m } from '$lib/paraglide/messages';

	let score = $state(0);
	let selectedSymbol = $state<SymbolName>();
	let opponentSymbol = $state<SymbolName>();
	let result = $state<'win' | 'lose' | 'tie'>();
	let timeLeft = $state(3);

	function resetGame() {
		selectedSymbol = undefined;
		opponentSymbol = undefined;
		result = undefined;
		timeLeft = 3;
	}

	function selectSymbol(symbol: SymbolName) {
		selectedSymbol = symbol;

		const intervalId = setInterval(() => {
			if (timeLeft === 1) {
				clearInterval(intervalId);

				const symbols: SymbolName[] = ['paper', 'rock', 'scissors'];
				const randomIndex = Math.floor(Math.random() * symbols.length);
				opponentSymbol = symbols[randomIndex];

				if (selectedSymbol === opponentSymbol) {
					result = 'tie';
					return;
				}

				if (
					(selectedSymbol === 'rock' && opponentSymbol === 'scissors') ||
					(selectedSymbol === 'paper' && opponentSymbol === 'rock') ||
					(selectedSymbol === 'scissors' && opponentSymbol === 'paper')
				) {
					score += 1;
					result = 'win';
					return;
				}

				result = 'lose';
				return;
			}

			timeLeft -= 1;
		}, 1000);
	}
</script>

<div class="flex flex-col items-center p-8 sm:py-12">
	<div class="w-full max-w-2xl">
		<Header {score} />
	</div>

	{#if !selectedSymbol}
		<div class="relative mx-auto mt-20 w-full max-w-xs sm:max-w-lg">
			<svg viewBox="0 0 476 430" fill="none">
				<path
					opacity="0.2"
					fill-rule="evenodd"
					clip-rule="evenodd"
					d="M381.5 99.5C381.5 99.5 89.8951 99.5 94.5739 99.5C99.2526 99.5 242.466 353.5 242.466 353.5L381.5 99.5Z"
					stroke="black"
					stroke-width="15"
				/>
			</svg>
			<div class="absolute top-0 left-0">
				<Symbol name="paper" onclick={() => selectSymbol('paper')} />
			</div>
			<div class="absolute top-0 right-0">
				<Symbol name="scissors" onclick={() => selectSymbol('scissors')} />
			</div>
			<div class="absolute bottom-0 flex w-full justify-center">
				<Symbol name="rock" onclick={() => selectSymbol('rock')} />
			</div>
		</div>
	{:else}
		<div
			class="mt-25 grid w-full grid-cols-2 gap-x-10 sm:max-w-xl lg:flex lg:max-w-fit lg:justify-between lg:gap-x-20"
		>
			<div
				class="flex flex-col items-center gap-y-4 sm:flex-col-reverse sm:gap-y-16 sm:place-self-start"
			>
				<Symbol name={selectedSymbol} size="lg" />
				<h3 class="font-bold tracking-[3px] text-white uppercase sm:text-2xl">{m.you_picked()}</h3>
			</div>
			<div
				class="flex h-full flex-col items-center justify-between gap-y-4 sm:flex-col-reverse sm:gap-y-16 sm:place-self-end lg:order-last lg:place-self-stretch"
			>
				{#if opponentSymbol}
					<Symbol size="lg" name={opponentSymbol} />
				{:else}
					<SymbolPlaceholder size="lg" {timeLeft} />
				{/if}
				<h3 class="font-bold text-white uppercase sm:text-2xl">{m.opponent_picked()}</h3>
			</div>

			{#if result}
				<div class="order-last col-span-2 -mx-4 mt-16 sm:mt-0 lg:order-0 lg:flex lg:items-center">
					<Result {result} playAgain={resetGame} />
				</div>
			{/if}
		</div>
	{/if}
</div>
