<script lang="ts">
	interface Props {
		size: 'sm' | 'lg';
		timeLeft: number;
	}

	let { timeLeft, size = 'sm' }: Props = $props();
</script>

<div
	class={[
		'relative flex items-center justify-center',
		size === 'sm' && 'w-32 sm:w-50',
		size === 'lg' && 'w-32 sm:w-50 lg:w-75',
	]}
>
	<svg viewBox="0 0 293 287" fill="none">
		<circle opacity="0.3" cx="146.306" cy="146.305" r="112.315" fill="black" />
	</svg>
	<span class="absolute text-4xl sm:text-6xl lg:text-8xl font-bold text-white">{timeLeft}</span>
</div>
