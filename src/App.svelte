<script lang="ts">
import Starfield from './Starfield.svelte';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { TextPlugin } from 'gsap/TextPlugin';
import textarray from './lib/text.js';
import { onMount } from 'svelte';

let bodysize = [document.body.clientWidth, document.body.clientHeight];
window.onresize = () => (bodysize = [document.body.clientWidth, document.body.clientHeight]);

onMount(() => {
	// ======= GSAP Animation Scripts
	// init & helper fns
	gsap.registerPlugin(ScrollTrigger, TextPlugin);
	var width = document.body.clientWidth;
	// Helper function for removing elements.
	function removeElement(element) {
		if (typeof element === 'string') {
			element = document.querySelector(element);
		}
		return function () {
			element.parentNode.removeChild(element);
		};
	}

	// text panel typewriter loop
	const textpanels = gsap.utils.toArray('.paneltext') as HTMLElement[];

	for (let t of textpanels) {
		gsap.to(t, {
			duration: 10,
			text: {
				value: textarray[t.id],
				speed: 0.8,
			},
			ease: 'none',
			scrollTrigger: {
				trigger: t,
				preventOverlaps: true,
			},
		});
	}

	// Custom(#intro)        Intro scrolling ship anim.
	gsap.to('#introtext', {
		duration: 3,
		delay: 2,
		text: 'Starship',
	});

	var introtl = gsap.timeline({ repeat: 0 });
	introtl
		.to('#introdiv', { x: 0.6 * width, duration: 20, ease: 'none' })
		.to('#introdiv', { opacity: 0, duration: 1 })
		.call(removeElement('#introdiv'));

	// Custom(#messenger)    appearing messenger boxes
	var messtl = gsap.timeline({
		scrollTrigger: {
			trigger: '#messengerdiv',
			pin: true,
			start: 'center center',
			end: '+=200%',
			scrub: 0.2,
			once: true,
		},
	});
	messtl
		.from('#mb1', { opacity: 0, scale: 0.4, x: -100, duration: 0.2, ease: 'power3' })
		.from('#mb2', {
			opacity: 0,
			scale: 0.4,
			x: -100,
			duration: 0.2,
			delay: 0.5,
			ease: 'power3',
		})
		.from('#mb3', { opacity: 0, scale: 0.4, x: -100, duration: 0.2, delay: 1, ease: 'power3' })
		.addDelay(3);
});
</script>

<!----------------------------------------------------------------------HTML--->

{#key bodysize}
	<Starfield />
{/key}

<div class="contentcontainer">
	<!-- Intro Scrolling Ship -->
	<div class="contentcontainer" style="height:150vh">
		<div
			id="introdiv"
			class="contentcontainer"
			style="width:100px; position:absolute; top:60vh; left:20vw"
		>
			<img src="image/heroship.png" style="object-fit:contain; width:100%" />
			<div
				id="introtext"
				class="introtext"
				style=" color:white;
                                font-family: 'Space Mono', monospace;
                                text-align:right;
                                position:relative;
                                font-size:1em"
			/>
		</div>
	</div>
	<!-- Lg Ship Image  -->
	<div><img class="panel" src="image/shiplg.png" /></div>
	<!-- ######### -->
	<div class="contentspacer" style="height:50vh" />
	<!-- atPC      -->
	<div class="paneltextdiv"><p class="paneltext low" id="atPC" /></div>
	<div><img class="panel" src="image/atPC.png" /></div>
	<div class="contentspacer" style="height:80vh" />
	<!-- etron      -->
	<div class="paneltextdiv"><p class="paneltext low" id="etron" /></div>
	<div><img class="panel" src="image/etron.png" /></div>
	<div class="contentspacer" style="height:100vh" />
	<!-- messenger -->
	<div id="messengerdiv">
		<div class="paneltextdiv" style="min-height: 10vh;">
			<p class="paneltext" id="messenger" style="height: 10vh;" />
		</div>
		<div id="messengerbox" style="position:relative; height:60vh; width:40.73vh; margin:auto;">
			<img
				src="image/messenger.png"
				style="position:absolute; left:0; height:100%; width:100%"
			/>
			<img
				id="mb1"
				src="image/messenger-1.png"
				style="height:15%; max-width:40vh;object-fit:contain;position: absolute; top: 20%; right:5%"
			/>
			<img
				id="mb2"
				src="image/messenger-2.png"
				style="height:20%; max-width:40vh;object-fit:contain;position: absolute; top: 35%; left:5%; right:95%"
			/>
			<img
				id="mb3"
				src="image/messenger-3.png"
				style="height:15%; max-width:40vh;object-fit:contain;position: absolute; top: 55%; right:5%"
			/>
		</div>
	</div>

	<div class="contentspacer" style="height:100vh" />

	<!-- outofroll 1&2      -->
	<div class="paneltextdiv"><p class="paneltext low" id="outofroll" /></div>
	<div class="contentspacer" style="height:50vh" />
	<div class="paneltextdiv"><p class="paneltext low" id="conservewaste" /></div>
	<div><img class="panel" src="image/conservewaste.png" /></div>
	<div class="contentspacer" style="height:100vh" />
	<!-- insta      -->
	<div class="paneltextdiv"><p class="paneltext low" id="insta" /></div>
	<div><img class="panel" src="image/instabody.png" /></div>
	<div class="paneltextdiv"><p class="paneltext" id="insta2" /></div>
	<div class="contentspacer" style="height:100vh" />
	<!-- chess      -->
	<div class="paneltextdiv"><p class="paneltext" id="chess" /></div>
	<div class="contentspacer" style="height:100vh" />
	<div><img class="panel" src="image/chess.png" /></div>
	<div class="paneltextdiv"><p class="paneltext" id="chess2" /></div>
	<div class="contentspacer" style="height:100vh" />
	<!-- clap clap&echo -->
	<div class="paneltextdiv"><p class="paneltext low" id="clapclap" /></div>
	<div><img class="panel" src="image/clapclap.png" /></div>
	<div class="paneltextdiv"><p class="paneltext low" id="clapecho" /></div>
	<div><img class="panel" src="image/clapecho.png" /></div>
	<div class="contentspacer" style="height:100vh" />
	<!-- quiz -->
	<div class="paneltextdiv"><p class="paneltext low" id="quiz" /></div>
	<div><img class="panel" src="image/quiz.png" /></div>
	<div class="paneltextdiv"><p class="paneltext" id="quiz2" /></div>
	<div class="contentspacer" style="height:70vh" />
	<div><img class="panel" src="image/trimup.png" /></div>
	<div class="contentspacer" style="height:200vh" />
	<!-- one with the ship -->
	<div><img class="panel" src="image/bounce.png" /></div>
	<div class="paneltextdiv"><p class="paneltext" id="onewiththeship" /></div>
	<div class="contentspacer" style="height:100vh" />
	<!-- barratt -->
	<div class="paneltextdiv"><p class="paneltext" id="barratt" /></div>
	<div class="contentspacer" style="height:100vh" />
	<!-- the light -->
	<div class="paneltextdiv"><p class="paneltext" id="thelight" /></div>
	<div class="contentspacer" style="height:100vh" />
	<div class="paneltextdiv"><p class="paneltext" id="thelight2" /></div>
	<div class="paneltextdiv">
		<p
			class="paneltext"
			id="thelight3"
			style="font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif"
		/>
	</div>
	<!-- ######## -->
	<div class="contentspacer" style="height:200vh" />
	<!-- end (pilot message) -->
	<div class="paneltextdiv"><p class="paneltext" id="end" /></div>
</div>

<style>
/* #region CONTENT SECTIONS/ROWS  */

.contentcontainer {
	display: block;
	position: relative;
	width: 100%;
	text-align: center;
}

.panel {
	display: block;
	width: min(90%, 900px);
	margin: auto;
	height: auto;
	object-fit: contain;
}

.paneltextdiv {
	height: 8em;
	position: relative;
	text-align: center;
	width: min(90%, 28em);
	margin-left: auto;
	margin-right: auto;
}
.paneltext {
	position: relative;
	color: white;
}

.low {
	position: relative;
}

.contentspacer {
	height: 10vh;
}

/* #endregion */
</style>
