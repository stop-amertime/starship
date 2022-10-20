<script lang="ts">
export let id: string;
export let low: boolean = false;
export let style = '';
</script>

<div class="paneltextdiv"><p class="paneltext" class:low {id} {style} /></div>

<style>
.paneltextdiv {
	height: 8em;
	position: relative;
	text-align: center;
	width: min(80%, 25em);
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
</style>
