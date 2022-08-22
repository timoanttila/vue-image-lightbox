<script>
export default {
	name: 'Lightbox',
	data() {
		return {
			images: ['example1.jpg','example2.jpg','example3.jpg'],
			imgKey: 0,
			lightboxActive: false
		}
	},
 	methods: {
		changeImage(key) {
			const count = this.images.length;
			if (key < 0) {
				this.imageKey = count - 1;
			} else if (key >= count) {
				this.imageKey = 0;
			} else {
				this.imageKey = key;
			}
    }   
	}
}
</script>

<template>
  <div id="lightboxExample">
		<div v-if="lightboxActive" id="overlay">
			<div id="overlayContent">
				<img class="block max-w-full max-h-screen object-scale-down mx-auto p-4" :src="page.images[imgKey]" alt="moi" />
			</div>

			<div id="overlayButtons" class="absolute bottom-4 right-10 z-40 text-right" :class="{ small: page.images.length == 1 }">
				<template v-if="page.images.length > 1">
					<button @click="changeImage(imgKey - 1)">
						<span>&lsaquo;</span>
					</button>
					<button @click="changeImage(imgKey + 1)">
						<span>&rsaquo;</span>
					</button>
				</template>
				<button class="close grid" @click="lightboxActive = false">
					<span class="self-center">X</span>
				</button>
			</div>
		</div>
    
    <button @click="lightboxActive = true" class="relative p-0 bg-transparent border border-solid border-gray-200">
      <img v-if="page.images" width="400" :src="page.images[imgKey]" :alt="`Tuotekuva ${page.name}`" loading="lazy" />
    </button>
  </div>
</template>

<style lang="scss">
#overlay {
	position: fixed;
	top: 0;
	left: 0;
	z-index: 120;
	width: 100vw;
	height: 100vh;
	overflow: hidden;
	background-color: rgba(0, 0, 0, .9);
}

#overlayButtons {
	display: grid;
	gap: 5px;
  
  &:not(.small) {
		grid-template-columns: repeat(3, 1fr);
	}

	button {
		width: 48px;
		height: 48px;
		border: 0;
		background-color: var(--primary);
		border: 2px solid #fff;
		color: #fff;
		font-weight: 700;
		padding: 0;
		display: grid;

		&:not(.close) span {
			width: 44px;
			margin-top: -4px;
			display: block;
			font-size: 32px;

			span {
				font-size: 24px;
			}
		}
	}
}
</style>
