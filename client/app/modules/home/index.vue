<template lang="pug">
	.container
			//- section
			//- 	fieldset
			//- 	.content.flex.align-center
			//- 		.card
			//- 			.block
			//- 				.title test
			//- 					audio(src='/mp3/juicy.mp3', preload='auto')
			section
				fieldset
				.content.flex.align-center
					.card
						.block
							.title youtube
									div(id='app1')
										my-component



</template>

<script>
'use strict'
import Vue from 'vue'
import VueYouTubeEmbed from 'vue-youtube-embed'
Vue.use(VueYouTubeEmbed)

Vue.component('my-component', {
	template: '<div><section><h2>listening events</h2><youtube :video-id="videoId" @ready="ready" @playing="playing"></youtube></section><section><h2>add options</h2><youtube :video-id="videoId" player-width="1280" player-height="750" :player-vars="{autoplay: 1}"></youtube></section></div>',
	data: function() {
		return {
			videoId: '3M_5oYU-IsU'
		}
	},
	methods: {
    ready (player) {
      this.player = player
    },
    playing (player) {
      // The player is playing a video.
    },
    change () {
      // when you change the value, the player will also change.
      // If you would like to change `playerVars`, please change it before you change `videoId`.
      // If `playerVars.autoplay` is 1, `loadVideoById` will be called.
      // If `playerVars.autoplay` is 0, `cueVideoById` will be called.
      this.videoId = 'another video id'
    },
    stop () {
      this.player.stopVideo()
    },
    pause () {
      this.player.pauseVideo()
    }
  }
})


</script>


