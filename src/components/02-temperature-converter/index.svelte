<script lang="ts">
	class Temperature {
		#c = $state(0)
		#f = $state(32)

		get c(){
			return this.#c
		}

		set c(c) {
			this.#c = c
			this.#f = c * (9 / 5) + 32
		}

		get f() {
			return this.#f
		}

		set f(f) {
			this.#f = f
			this.#c = (f - 32) * (5 / 9)
		}
	}

	const temperature = new Temperature()
</script>

<div>
	<input type="number" bind:value={temperature.c} /> ° C = 
	<input type="number" bind:value={temperature.f}/> ° F
</div>

<style>
	input[type="number"] {
		max-width: 10ch;
		color: black;
		margin-right: 1ch;
	}
</style>