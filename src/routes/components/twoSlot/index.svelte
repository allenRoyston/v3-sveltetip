<script lang="ts">
	import LibrarySnippet from '@component/base/LibrarySnippet.svelte';

	import TwoSlot from '@layout/TwoSlot.svelte';

	let propstr = '';
	let selectstr = '';
	let inputstr = '';
	let props;
	let selectprops;
	let inputprops;

	const snippet = {
		name: 'TwoSlot',
		importName: '@base/TwoSlot.svelte',
		props: {
			hideLeft: false,
			hideRight: false,
			outline: true,
			rounded: true,
			nopadding: false
		},
		inputs: [
			{
				forprop: 'style',
				renderAs: 'input',
				componentprop: { type: 'text', placeholder: 'outline: 1px solid red' },
				value: null
			}
		]
	};

	$: livecode = `    
    <TwoSlot${propstr}${selectstr}${inputstr}>
      <h2 slot='left'>Left</h2>

      <div slot='right'>
        <button>On the Right</button>
      </div>
    </TwoSlot>   
     `;
</script>

<LibrarySnippet
	{...snippet}
	{livecode}
	bind:propstr
	bind:selectstr
	bind:inputstr
	bind:props
	bind:selectprops
	bind:inputprops
>
	<div slot="liveexample">
		<TwoSlot {...props} {...selectprops} {...inputprops}>
			<h2 slot="left">Left</h2>

			<div slot="right">
				<button>On the Right</button>
			</div>
		</TwoSlot>
	</div>
</LibrarySnippet>
