<script lang="ts">
	const katakana = [
		'ア',
		'イ',
		'ウ',
		'エ',
		'オ',
		'カ',
		'キ',
		'ク',
		'ケ',
		'コ',
		'サ',
		'シ',
		'ス',
		'セ',
		'ソ',
		'タ',
		'チ',
		'ツ',
		'テ',
		'ト',
		'ナ',
		'ニ',
		'ヌ',
		'ネ',
		'ノ',
		'ハ',
		'ヒ',
		'フ',
		'ヘ',
		'ホ',
		'マ',
		'ミ',
		'ム',
		'メ',
		'モ',
		'ヤ',
		'ユ',
		'ヨ',
		'ラ',
		'リ',
		'ル',
		'レ',
		'ロ',
		'ワ',
		'ヲ',
		'ン',
		'ガ',
		'ギ',
		'グ',
		'ゲ',
		'ゴ',
		'ザ',
		'ジ',
		'ズ',
		'ゼ',
		'ゾ',
		'ダ',
		'ヂ',
		'ヅ',
		'デ',
		'ド',
		'バ',
		'ビ',
		'ブ',
		'ベ',
		'ボ',
		'パ',
		'ピ',
		'プ',
		'ペ',
		'ポ',
		'ャ',
		'ュ',
		'ョ',
		'ッ'
	];

	function shuffle(array: string[]): string[] {
		const shuffled: string[] = [...array];
		for (let i = shuffled.length - 1; i > 0; i--) {
			const j = Math.floor(Math.random() * (i + 1));
			[shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
		}
		return shuffled;
	}

	let currentKatakana: string = shuffle(katakana)[0];
	let userAnswer = '';

	function checkAnswer() {
		type RomajiMap = { [katakana: string]: string };
		const romajiMap: RomajiMap = {
			ア: 'a',
			イ: 'i',
			ウ: 'u',
			エ: 'e',
			オ: 'o',
			カ: 'ka',
			キ: 'ki',
			ク: 'ku',
			ケ: 'ke',
			コ: 'ko',
			サ: 'sa',
			シ: 'shi',
			ス: 'su',
			セ: 'se',
			ソ: 'so',
			タ: 'ta',
			チ: 'chi',
			ツ: 'tsu',
			テ: 'te',
			ト: 'to',
			ナ: 'na',
			ニ: 'ni',
			ヌ: 'nu',
			ネ: 'ne',
			ノ: 'no',
			ハ: 'ha',
			ヒ: 'hi',
			フ: 'fu',
			ヘ: 'he',
			ホ: 'ho',
			マ: 'ma',
			ミ: 'mi',
			ム: 'mu',
			メ: 'me',
			モ: 'mo',
			ヤ: 'ya',
			ユ: 'yu',
			ヨ: 'yo',
			ラ: 'ra',
			リ: 'ri',
			ル: 'ru',
			レ: 're',
			ロ: 'ro',
			ワ: 'wa',
			ヲ: 'wo',
			ン: 'n',
			ガ: 'ga',
			ギ: 'gi',
			グ: 'gu',
			ゲ: 'ge',
			ゴ: 'go',
			ザ: 'za',
			ジ: 'ji',
			ズ: 'zu',
			ゼ: 'ze',
			ゾ: 'zo',
			ダ: 'da',
			ヂ: 'ji',
			ヅ: 'zu',
			デ: 'de',
			ド: 'do',
			バ: 'ba',
			ビ: 'bi',
			ブ: 'bu',
			ベ: 'be',
			ボ: 'bo',
			パ: 'pa',
			ピ: 'pi',
			プ: 'pu',
			ペ: 'pe',
			ポ: 'po',
			ャ: 'ya',
			ュ: 'yu',
			ョ: 'yo',
			ッ: 'tsu'
		};
		const currentRomaji: string = romajiMap[currentKatakana];
		if (userAnswer === currentRomaji) {
			const index: number = katakana.indexOf(currentKatakana);
			currentKatakana = shuffle(katakana)[(index + 1) % katakana.length];
			userAnswer = '';
			const messageElement: HTMLElement | null = document.getElementById('message');
			if (messageElement) {
				messageElement.textContent = 'Correct!';
				messageElement.style.color = 'green';
			}
			const currentKatakanaElement: HTMLElement | null = document.getElementById('currentKatakana');
			if (currentKatakanaElement) {
				currentKatakanaElement.textContent = currentKatakana;
			}
		} else {
			const messageElement: HTMLElement | null = document.getElementById('message');
			if (messageElement) {
				messageElement.textContent = 'Incorrect, réessayez!';
				messageElement.style.color = 'red';
			}
		}
	}
</script>

<div class="mt-8 text-white text-3xl text-center font-semibold space-x-24">
	<a data-sveltekit-preload-data="tap" href="/" class="hover:text-blue-300"> Acceuil </a>

	<a data-sveltekit-preload-data="tap" href="/hiragana" class="hover:text-blue-300"> Hiragana </a>
</div>

<div class="flex flex-col justify-center items-center mt-8">
	<h1 class="text-8xl font-bold text-white">{currentKatakana}</h1>

	<div class="mt-8">
		<form
			class="text-3xl flex flex-col justify-center items-center text-white"
			on:submit|preventDefault={checkAnswer}
		>
			<label for="answer" class="font-semibold">Réponse:</label>
			<input
				type="text"
				id="answer"
				class="mt-4 rounded-lg text-black font-medium"
				bind:value={userAnswer}
			/>
			<button
				type="submit"
				class="mt-4 bg-blue-500 p-4 rounded-2xl font-semibold hover:bg-blue-600 active:bg-blue-700"
				>Envoyer</button
			>
		</form>

		<div id="message" class="mt-4 flex justify-center items-center font-bold text-2xl" />
	</div>
</div>

<style lang="postcss">
	:global(html) {
	}
</style>
