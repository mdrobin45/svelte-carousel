<script>
	let images = [];
	let currentSlide = 0;

	fetch('./slides.json')
		.then((res) => res.json())
		.then((data) => {
			images = data;
		});

	// Next navigation
	const nextSlide = () => {
		currentSlide = (currentSlide + 1) % images.length;
	};

	// Prev navigation
	const prevSlide = () => {
		currentSlide = (currentSlide - 1 + images.length) % images.length;
	};
	$: console.log(images.length);
</script>

<!-- Slider HTML -->
<div class="slider">
	{#if images.length > 0}
		<div class="slide">
			<img src={images[currentSlide].src} alt="" />
		</div>
		<button on:click={nextSlide} class="btn btn-next"
			><svg xmlns="http://www.w3.org/2000/svg" width="0.5em" height="1em" viewBox="0 0 12 24"
				><defs
					><path
						id="weuiArrowOutlined0"
						fill="currentColor"
						d="m7.588 12.43l-1.061 1.06L.748 7.713a.996.996 0 0 1 0-1.413L6.527.52l1.06 1.06l-5.424 5.425z"
					/></defs
				><use
					fill-rule="evenodd"
					href="#weuiArrowOutlined0"
					transform="rotate(-180 5.02 9.505)"
				/></svg
			></button
		>
		<button on:click={prevSlide} class="btn btn-prev"
			><svg xmlns="http://www.w3.org/2000/svg" width="1em" height="1em" viewBox="0 0 32 32"
				><path
					fill="currentColor"
					d="m19.031 4.281l-11 11l-.687.719l.687.719l11 11l1.438-1.438L10.187 16L20.47 5.719z"
				/></svg
			></button
		>
	{:else}
		<p>Loading...</p>
	{/if}
</div>

<!-- Styles -->
<style>
	.slider {
		width: 100%;
		height: 85vh;
		position: relative;
		overflow: hidden;
	}

	.slide {
		width: 100%;
		position: absolute;
		transition: all 0.5s;
	}

	.slide img {
		width: 100%;
		height: 100%;
		object-fit: cover;
	}

	.btn {
		position: absolute;
		width: 40px;
		height: 40px;
		padding: 10px;
		border: none;
		border-radius: 50%;
		z-index: 10px;
		cursor: pointer;
		background-color: #fff;
		font-size: 18px;
	}
	.btn:active {
		transform: scale(1.1);
	}
	.btn-prev {
		top: 45%;
		left: 2%;
	}

	.btn-next {
		top: 45%;
		right: 2%;
	}
</style>
