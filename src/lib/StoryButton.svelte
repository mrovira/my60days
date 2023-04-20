<script>
	
	let buttonProps = {
	class:[$$restProps.class]
	}
</script>
	<button on:click
			
			>
			<slot/>
	</button>

<style>
	.primary{
		color:green;
	}

	.sm {
		font-size:1em;
		padding:0.1em;
	}

</style>