<template lang="pug">
	.container
		h1 Music Player

		.guide
			section
				fieldset
					.content.flex.align-center
						.card
							.block
								.title Play Music
								p This is where you can play music. Make sure to search for music first.
							.block
								small.text-muted Last updated 5 mins ago

			section
				fieldset
					.content.flex.align-center
						.card
							.block
								.title My Music
									#app
										#instructions
											h3 Try clicking on the cover image and then on the screen that will show up
										|
										img#cover(:src='cover', alt='Cover', @click='coverClicked', :class='coverClass')
										|
										#infoPage(:class='infoPage', @click='infoPageClicked')
											.content
											h1 {{songName}}
											|
											h3 {{artistName}}
										|
										#player(:style='playerStyle')
											#filter
											|
											#controls(:class='controls')
											img#backwardButton(@click='backwardButtonClicked', src='data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHZpZXdCb3g9IjAgMCAxMjkgMTI5IiBlbmFibGUtYmFja2dyb3VuZD0ibmV3IDAgMCAxMjkgMTI5IiB3aWR0aD0iMTI4cHgiIGhlaWdodD0iMTI4cHgiPgogIDxnPgogICAgPGc+CiAgICAgIDxwYXRoIGQ9Im02NC41LDEyMi42YzMyLDAgNTguMS0yNiA1OC4xLTU4LjFzLTI2LTU4LTU4LjEtNTgtNTgsMjYtNTgsNTggMjYsNTguMSA1OCw1OC4xem0wLTEwOGMyNy41LDUuMzI5MDdlLTE1IDQ5LjksMjIuNCA0OS45LDQ5LjlzLTIyLjQsNDkuOS00OS45LDQ5LjktNDkuOS0yMi40LTQ5LjktNDkuOSAyMi40LTQ5LjkgNDkuOS00OS45eiIgZmlsbD0iIzAwMDAwMCIvPgogICAgICA8cGF0aCBkPSJtNzAsOTMuNWMwLjgsMC44IDEuOCwxLjIgMi45LDEuMiAxLDAgMi4xLTAuNCAyLjktMS4yIDEuNi0xLjYgMS42LTQuMiAwLTUuOGwtMjMuNS0yMy41IDIzLjUtMjMuNWMxLjYtMS42IDEuNi00LjIgMC01LjhzLTQuMi0xLjYtNS44LDBsLTI2LjQsMjYuNGMtMC44LDAuOC0xLjIsMS44LTEuMiwyLjlzMC40LDIuMSAxLjIsMi45bDI2LjQsMjYuNHoiIGZpbGw9IiMwMDAwMDAiLz4KICAgIDwvZz4KICA8L2c+Cjwvc3ZnPgo=')
											|
											img#playPauseButton(:src='playPauseButton', @click='playPauseClicked', :class='faded')
											|
											img#forwardButton(@click='forwardButtonClicked', src='data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTYuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgd2lkdGg9IjEyOHB4IiBoZWlnaHQ9IjEyOHB4IiB2aWV3Qm94PSIwIDAgNjEyIDYxMiIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgNjEyIDYxMjsiIHhtbDpzcGFjZT0icHJlc2VydmUiPgo8Zz4KCTxnPgoJCTxwYXRoIGQ9Ik01ODcuNTcyLDE4Ni44ODFjLTMyLjI2Ni03NS4yMjUtODcuMDk2LTEyOS45MzQtMTYyLjk1Ni0xNjIuMjg1QzM4Ni43MTEsOC40MjcsMzQ2Ljk4NSwwLjE2OCwzMDUuNDk3LDAuMTY4ICAgIGMtNDEuNDg4LDAtODAuOTE0LDguMTgxLTExOC43ODQsMjQuNDI4QzExMS40ODgsNTYuODYxLDU2LjQxNSwxMTEuNTM1LDI0LjA5MiwxODYuODgxQzcuODk1LDIyNC42MjksMCwyNjQuMTc2LDAsMzA1LjY2NCAgICBjMCw0MS40OTYsNy44OTUsODEuMzcxLDI0LjA5MiwxMTkuMTI3YzMyLjMyMyw3NS4zNDYsODcuMzk2LDEzMC4zNDgsMTYyLjYyMSwxNjIuNjIxYzM3Ljg3LDE2LjI0Nyw3Ny4yOTUsMjQuNDIsMTE4Ljc4NCwyNC40MiAgICBjNDEuNDg5LDAsODEuMjE0LTguMjU5LDExOS4xMi0yNC40MmM3NS44Ni0zMi4zNTIsMTMwLjY5LTg3LjQwMywxNjIuOTU2LTE2Mi42MjFDNjAzLjgxOSwzODYuOTE0LDYxMiwzNDcuMTYsNjEyLDMwNS42NjQgICAgQzYxMiwyNjQuMTc2LDYwMy44MTksMjI0Ljc1Nyw1ODcuNTcyLDE4Ni44ODF6IE01MzguNzE3LDQ0MC44NTNjLTI0LjAxNCw0MS4xOTUtNTYuOTIyLDczLjg3Ni05OC4zNzUsOTguMDM5ICAgIGMtNDEuMTk2LDI0LjAyMS04Ni4zMjUsMzYuMTM1LTEzNC44NDUsMzYuMTM1Yy0zNi40NywwLTcxLjI3LTcuMDI0LTEwNC4zOTktMjEuNDE1Yy0zMy4xMjMtMTQuMzg0LTYxLjczMy0zMy4yOTQtODUuNjYyLTU3LjIxNSAgICBjLTIzLjkyMS0yMy45MjgtNDIuOTY2LTUyLjgxMS01Ny4yMTQtODUuOTk3Yy0xNC4xOTgtMzMuMDY1LTIxLjA4LTY4LjI1OC0yMS4wOC0xMDQuNzM1YzAtNDguNTIsMTEuOTIxLTkzLjQyOCwzNS43OTktMTM0LjUwOSAgICBjMjMuOTcxLTQxLjIzMSw1Ni44ODYtNzMuOTQ3LDk4LjA0LTk4LjA0YzQxLjE2LTI0LjA5Miw4NS45OTctMzYuMTQyLDEzNC41MTctMzYuMTQyczkzLjY0OSwxMi4xMjEsMTM0Ljg0NSwzNi4xNDIgICAgYzQxLjQ1MywyNC4xNjQsNzQuMjgzLDU2Ljg3OSw5OC4zNzUsOTguMDRjMjQuMDkyLDQxLjE1MywzNi4xNDIsODUuOTksMzYuMTQyLDEzNC41MDkgICAgQzU3NC44NTgsMzU0LjE4NSw1NjIuODg4LDM5OS4zOTksNTM4LjcxNyw0NDAuODUzeiIgZmlsbD0iIzAwMDAwMCIvPgoJCTxwYXRoIGQ9Ik0yNzAuMDI2LDEyOC45OTVjLTcuNjAzLTcuNzk1LTE5LjQwMi03LjM2Ny0yNi4wOTgtMC42NzFjLTcuNjk1LDcuNjk1LTcuMjc0LDE4Ljk4MS0wLjY3MSwyNS43NjNsMTQ5LjU3MSwxNTMuNTkxICAgIEwyNDMuMjU3LDQ1Ny4yNDJjLTcuMjEsNy4yMTctNi42ODksMTkuMDc0LDAsMjUuNzdjMy42ODMsMy42NzcsOC4zNjYsNS42ODksMTMuNzIsNS42ODljNS4wMTksMCw5LjM2Ni0yLjAyMSwxMy4wNDktNS42ODkgICAgbDE2Mi4yODYtMTYxLjYyMWM3LjIzLTcuMTk1LDYuNjA5LTE5LjMyNCwwLTI2LjA5OEwyNzAuMDI2LDEyOC45OTV6IiBmaWxsPSIjMDAwMDAwIi8+Cgk8L2c+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPC9zdmc+Cg==')

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
									section
											h2 listening events
											|
											youtube(:video-id='videoId', @ready='ready', @playing='playing')
									section
											h2 add options
											|
											youtube(:video-id='videoId', player-width='1280', player-height='750', :player-vars='{autoplay: 1}')



</template>

<script>
'use strict'
import Vue from 'vue'
import VueYouTubeEmbed from 'vue-youtube-embed'
Vue.use(VueYouTubeEmbed)

const app = new Vue({
  el: '#app1',
  data: {
    videoId: '3M_5oYU-IsU',
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


