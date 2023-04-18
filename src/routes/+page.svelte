<script>
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
		'ぁ',
		'ぃ',
		'ぅ',
		'ぇ',
		'ぉ',
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
			ぁ: 'a',
			ぃ: 'i',
			ぅ: 'u',
			ぇ: 'e',
			ぉ: 'o',
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
			alert('Correct!');
			document.getElementById('currentHiragana').innerHTML = currentHiragana;
		} else {
			alert('Faux!');
		}
	}
</script>

<h1 class="text-6xl font-bold flex flex-col justify-center items-center mt-8">{currentHiragana}</h1>

<form
	class="text-3xl flex flex-col justify-center items-center mt-8"
	on:submit|preventDefault={checkAnswer}
>
	<label class="font-bold" for="answer">Réponse :</label>
	<input
		class="mt-4 rounded-2xl focus:outline-none border-4 border-black"
		type="text"
		id="answer"
		bind:value={userAnswer}
	/>
	<button
		type="submit"
		class="mt-4 bg-blue-500 p-4 text-sm rounded-2xl border-4 border-black hover:bg-blue-700 active:bg-blue-900"
		>Envoyer</button
	>
</form>

<style lang="postcss">
	:global(html) {
	}
</style>
