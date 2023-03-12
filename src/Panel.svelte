<script lang="ts">
export let img: string;
let url = `image/${img}.png`;
</script>

<div><img class="panel" src={url} alt={'Image with label:' + img} /></div>

<style>
/* #region CONTENT SECTIONS/ROWS  */

.panel {
	display: block;
	width: min(80%, 400px);
	margin: auto;
	height: auto;
	object-fit: contain;
}
</style>
