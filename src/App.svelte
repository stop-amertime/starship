<script lang="ts">
import Text from './Text.svelte';

import Spacer from './Spacer.svelte';
import Panel from './Panel.svelte';

import Starfield from './Starfield.svelte';
import gsap from 'gsap';
import { ScrollTrigger } from 'gsap/ScrollTrigger';
import { TextPlugin } from 'gsap/TextPlugin';
import textarray from './lib/text.js';
import { onMount } from 'svelte';

let bodysize = [document.body.clientWidth, document.body.clientHeight];
window.onresize = () => (bodysize = [document.body.clientWidth, document.body.clientHeight]);

let low = true;

onMount(() => {
	// ======= GSAP Animation Scripts
	// init & helper fns
	gsap.registerPlugin(ScrollTrigger, TextPlugin);
	var width = document.body.clientWidth;

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
				speed: 1.5,
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
		duration: 4,
		delay: 2,
		text: 'Starship',
	});

	var introtl = gsap.timeline({ repeat: 0 });
	introtl
		.to('#introdiv', { x: 0.6 * width, duration: 10, ease: 'none' })
		.to('#introdiv', { opacity: 0, duration: 1 })
		.to('#scrollreminder', { opacity: 1, duration: 2 })
		.call(removeElement('#introdiv'));

	// Custom(#messenger)    appearing messenger boxes
	var messengerTimeline = gsap.timeline({
		scrollTrigger: {
			trigger: '#messengerdiv',
			pin: true,
			start: 'center center',
			end: '+=200%',
			scrub: 0.2,
			once: true,
		},
	});

	messengerTimeline
		.from('#mb1', {
			opacity: 0,
			scale: 0.4,
			x: -100,
			duration: 0.2,
			delay: 0.2,
			ease: 'power3',
		})
		.from('#mb2', {
			opacity: 0,
			scale: 0.4,
			x: -100,
			duration: 0.2,
			delay: 0.5,
			ease: 'power3',
		})
		.from('#mb3', {
			opacity: 0,
			scale: 0.4,
			x: -100,
			duration: 0.2,
			delay: 1,
			ease: 'power3',
		})
		.addPause('+=2');
});
</script>

<!----------------------------------------------------------------------HTML--->

{#key bodysize}
	<Starfield />
{/key}

<div class="wrapper">
	<!-- Intro: Ship Scrolling -->
	<div id="scrollreminder"><p>scroll down</p></div>
	<div class="wrapper" style="height:150vh">
		<div id="introdiv" class="intro wrapper">
			<img
				src="image/heroship.png"
				alt="A Spaceship flying through stars"
				style="object-fit:contain; width:100%"
			/>
			<p id="introtext" class="introtext" />
		</div>
	</div>

	<!-- Zoomed In Image of Ship   -->
	<Panel img="shiplg" />
	<Spacer height="50vh" />

	<!-- Captain At PC      -->
	<Text id="atPC" {low} />
	<Panel img="atPC" />
	<Spacer height="80vh" />

	<!-- EntertainoTron      -->
	<Text id="etron" {low} />
	<Panel img="etron" />
	<Spacer height="100vh" />

	<!-- Messenger App -->
	<div id="messengerdiv">
		<div class="paneltextdiv" style="min-height: 10vh;">
			<p class="paneltext" id="messenger" style="height: 10vh;" />
		</div>
		<div id="messengerbox" style="position:relative; height:60vh; width:40.73vh; margin:auto;">
			<img
				src="image/messenger.png"
				alt="An Instant Messaging Client"
				style="position:absolute; left:0; height:100%; width:100%"
			/>
			<img
				id="mb1"
				class="messagebox"
				src="image/messenger-1.png"
				alt="Messenger Box 1"
				style="height:15%; max-width:40vh;object-fit:contain;position: absolute; top: 20%; right:5%"
			/>
			<img
				id="mb2"
				class="messagebox"
				src="image/messenger-2.png"
				alt="Messenger Box 3"
				style="height:20%; max-width:40vh;object-fit:contain;position: absolute; top: 35%; left:5%; right:95%"
			/>
			<img
				id="mb3"
				class="messagebox"
				src="image/messenger-3.png"
				alt="Messenger Box 4"
				style="height:15%; max-width:40vh;object-fit:contain;position: absolute; top: 55%; right:5%"
			/>
		</div>
	</div>
	<Spacer height="100vh" />

	<!-- outofroll , conserve waste  -->
	<Text id="outofroll" {low} />
	<Spacer height="50vh" />
	<Text id="conservewaste" {low} />
	<Panel img="conservewaste" />
	<Spacer height="100vh" />

	<!-- insta      -->
	<Text id="insta" {low} />
	<Panel img="instabody" />
	<Text id="insta2" />
	<Spacer height="100vh" />

	<!-- chess      -->
	<Text id="chess" />
	<Spacer height="100vh" />
	<Panel img="chess" />
	<Text id="chess2" />
	<Spacer height="100vh" />

	<!-- clap clap&echo -->
	<Text id="clapclap" {low} />
	<Panel img="clapclap" />
	<Text id="clapecho" {low} />
	<Panel img="clapecho" />
	<Spacer height="100vh" />

	<!-- quiz -->
	<Text id="quiz" {low} />
	<Panel img="quiz" />
	<Text id="quiz2" />
	<Spacer height="70vh" />
	<Panel img="trimup" />
	<Spacer height="200vh" />

	<!-- one with the ship -->
	<Panel img="bounce" />
	<Text id="onewiththeship" />
	<Spacer height="100vh" />

	<!-- barratt -->
	<Text id="barratt" />
	<Spacer height="100vh" />

	<!-- the light -->
	<Text id="thelight" />
	<Spacer height="100vh" />
	<Text id="thelight2" />
	<Text
		id="thelight3"
		style="font-family:Cambria, Cochin, Georgia, Times, 'Times New Roman', serif"
	/>
	<Spacer height="200vh" />

	<!-- end (pilot message) -->
	<Text id="end" />
	<Spacer height="60vh" />
</div>

<style>
:global(p) {
	filter: drop-shadow(0px 0px 6px white);
	color: white;
}

.wrapper {
	display: block;
	position: relative;
	width: 100%;
	text-align: center;
}

.intro.wrapper {
	width: 100px;
	position: absolute;
	top: 60vh;
	left: 20vw;
}

#scrollreminder {
	position: absolute;
	width: 100vh;
	height: 50vh;
	opacity: 0;
}

#scrollreminder > p {
	position: absolute;
	bottom: 0;
	width: 100%;
	margin: auto;
}

.introtext {
	font-family: 'Space Mono', monospace;
	text-align: right;
	position: relative;
	font-size: 1em;
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

.messagebox {
	filter: drop-shadow(5px 10px 5px #222222);
}

/* #endregion */
</style>
