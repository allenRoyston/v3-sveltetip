<script lang="ts">
	import Accordion from '@layout/Accordion.svelte';
	export let title = null;
	export let flex = false;
</script>

<div class="library-block">
	<Accordion>
		<div slot="title" class="title">
			<h3>{title || 'Title'}</h3>
		</div>
		<div slot="content">
			<div class:hasFlex={flex}>
				<slot />
			</div>
		</div>
	</Accordion>
</div>

<style lang="scss">
	.library-block {
		.hasFlex {
			display: flex;
			gap: 10px;
			align-items: center;
			justify-content: flex-start;
		}
	}
</style>
