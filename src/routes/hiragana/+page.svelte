<script>
	// @ts-nocheck

	const hiragana = [
		'あ',
		'い',
		'う',
		'え',
		'お',
		'か',
		'き',
		'く',
		'け',
		'こ',
		'さ',
		'し',
		'す',
		'せ',
		'そ',
		'た',
		'ち',
		'つ',
		'て',
		'と',
		'な',
		'に',
		'ぬ',
		'ね',
		'の',
		'は',
		'ひ',
		'ふ',
		'へ',
		'ほ',
		'ま',
		'み',
		'む',
		'め',
		'も',
		'や',
		'ゆ',
		'よ',
		'ら',
		'り',
		'る',
		'れ',
		'ろ',
		'わ',
		'を',
		'ん',
		'が',
		'ぎ',
		'ぐ',
		'げ',
		'ご',
		'ざ',
		'じ',
		'ず',
		'ぜ',
		'ぞ',
		'だ',
		'ぢ',
		'づ',
		'で',
		'ど',
		'ば',
		'び',
		'ぶ',
		'べ',
		'ぼ',
		'ぱ',
		'ぴ',
		'ぷ',
		'ぺ',
		'ぽ',
		'ゃ',
		'ゅ',
		'ょ',
		'っ'
	];

	function shuffle(array) {
		for (let i = array.length - 1; i > 0; i--) {
			const j = Math.floor(Math.random() * (i + 1));
			[array[i], array[j]] = [array[j], array[i]];
		}
		return array;
	}
	let currentHiragana = shuffle(hiragana)[0];
	let userAnswer = '';
	console.log(currentHiragana);
	function checkAnswer() {
		const romajiMap = {
			あ: 'a',
			い: 'i',
			う: 'u',
			え: 'e',
			お: 'o',
			か: 'ka',
			き: 'ki',
			く: 'ku',
			け: 'ke',
			こ: 'ko',
			さ: 'sa',
			し: 'shi',
			す: 'su',
			せ: 'se',
			そ: 'so',
			た: 'ta',
			ち: 'chi',
			つ: 'tsu',
			て: 'te',
			と: 'to',
			な: 'na',
			に: 'ni',
			ぬ: 'nu',
			ね: 'ne',
			の: 'no',
			は: 'ha',
			ひ: 'hi',
			ふ: 'fu',
			へ: 'he',
			ほ: 'ho',
			ま: 'ma',
			み: 'mi',
			む: 'mu',
			め: 'me',
			も: 'mo',
			や: 'ya',
			ゆ: 'yu',
			よ: 'yo',
			ら: 'ra',
			り: 'ri',
			る: 'ru',
			れ: 're',
			ろ: 'ro',
			わ: 'wa',
			を: 'wo',
			ん: 'n',
			が: 'ga',
			ぎ: 'gi',
			ぐ: 'gu',
			げ: 'ge',
			ご: 'go',
			ざ: 'za',
			じ: 'ji',
			ず: 'zu',
			ぜ: 'ze',
			ぞ: 'zo',
			だ: 'da',
			ぢ: 'ji',
			づ: 'zu',
			で: 'de',
			ど: 'do',
			ば: 'ba',
			び: 'bi',
			ぶ: 'bu',
			べ: 'be',
			ぼ: 'bo',
			ぱ: 'pa',
			ぴ: 'pi',
			ぷ: 'pu',
			ぺ: 'pe',
			ぽ: 'po',
			ゃ: 'ya',
			ゅ: 'yu',
			ょ: 'yo',
			っ: 'tsu'
		};
		const currentRomaji = romajiMap[currentHiragana];
		if (userAnswer === currentRomaji) {
			const index = hiragana.indexOf(currentHiragana);
			currentHiragana = shuffle(hiragana)[(index + 1) % hiragana.length];
			userAnswer = '';
			document.getElementById('message').textContent = 'Correct!';
			document.getElementById('message').style.color = 'green';
			document.getElementById('currentHiragana').textContent = currentHiragana;
		} else {
			document.getElementById('message').textContent = 'Incorrect, réessayez!';
			document.getElementById('message').style.color = 'red';
		}
	}
</script>

<div class="mt-8 text-white text-3xl text-center font-semibold space-x-24">
	<a data-sveltekit-preload-data="tap" href="/" class="hover:text-blue-300"> Acceuil </a>

	<a data-sveltekit-preload-data="tap" href="/katakana" class="hover:text-blue-300"> Katakana </a>
</div>

<div class="flex flex-col justify-center items-center mt-8">
	<h1 class="text-8xl font-bold text-white">{currentHiragana}</h1>

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
