<script lang="ts">
	let count = $state(0)
</script>

<div>
	<div class="flex-gap">
		<input type="number" bind:value={count} readonly/>
		<button class="count" onclick={() => count++}>Count</button>
	</div>
	<button class="reset" onclick={() => count = 0}>Reset</button>
</div>


<style>
	input[type="number"] {
			color: black;
	}

  .count {
			color: #ff3f20;
	}

	.reset {
			box-shadow: none;
			text-shadow: none;
			transition: none;
			background: none;
			border: none;
			color: #ff3f20;
			text-decoration: underline;
			cursor: pointer;
			padding-top: 12px;
			margin-left: -20px;
	}
</style>