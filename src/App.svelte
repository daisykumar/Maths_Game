<script>
	
	let klasse = "faller"
	
	let tall1 = 9
	let tall2 = 5
	$: fasit = tall1 * tall2
	let svar = ""
	let theGameIsOn = true
	$: riktigsvar = (fasit === svar)
	$: regnestykke = `${tall1} x ${tall2}`
	let poeng = 0
	
	const lagNyeTall = () => {
		tall1 =  Math.ceil(Math.random() * 10)
		tall2 =  Math.ceil(Math.random() * 10)
	}
	
	const sjekkSvar = () => {
		if(riktigsvar && theGameIsOn) {
			lagNyeTall()
			svar = ""	
			klasse = ""
			poeng++
			setTimeout( () => { klasse = "faller" }, 50 )
		}
		
	}
	
	const gameOver = () => {
		theGameIsOn = false
		console.log("GAME OVER")
	}
	
</script>


<section>
	<header>
		<div class="points"><label>Your Points</label><p>{poeng}</p></div>
		<div class="points"><label>Highscore</label><p>0</p></div>
	</header>	
	
	<main>
		<div on:animationend={gameOver} class="{klasse}">{regnestykke}</div>	
	</main>
	
	<footer>
		<input type="number" bind:value={svar} on:input={sjekkSvar}>
	</footer>
	
</section>

<style>
	* {
		margin: 0;
		box-sizing: border-box;
	}
	section{
		display: grid;
		grid-template-rows: auto 300px auto;
		width: 350px;
		background-color: #eee;
		margin: 20px auto;
	}
	
	header{
		background-color: #f9e5bc;
		padding: 0.5em;
		display: grid;
		grid-template-columns: 1fr 1fr;
	}

	.points{
		text-align: center;
	}
	.points p {
		font-size: 2rem;
	}
	
	input {
		width: 100%;
		padding: 0.5rem;
		font-size: 1.75rem;
		text-align: center;
		border: none;
	}
	
	input:focus {
		outline: none;
	}
	
	footer {
		border: 4px solid lightblue;
	}
	
	@keyframes fallNed {
		to {
			transform: translateY(250px);
		}
	}

	.faller {
		animation: fallNed 4s linear forwards;
	}

	main div {
		width: 200px;
		height: 50px;
		line-height: 50px;
		margin: 10px auto;
		background-color: #90EE90;
		text-align: center;
		font-size: 2rem;
	}	
	
</style>