<script lang="ts">
	import { getContext } from 'svelte';
	import LibrarySnippet from '@component/base/LibrarySnippet.svelte';

	import Button from '@button/Button.svelte';
	import Link from '@link/Link.svelte';

	let propstr = '';
	let selectstr = '';
	let inputstr = '';
	let props;
	let selectprops;
	let inputprops;

	const snippet = {
		name: 'Snackbar',
		importName: '@system/Snackbar.svelte',
		props: {
			closeOnClick: false
		},
		dropdowns: [
			{
				label: 'applyTheme',
				options: ['primary', 'success', 'warning', 'danger'],
				value: 0
			}
		],
		inputs: [
			{ forprop: 'duration', renderAs: 'input', componentprop: { type: 'number' }, value: 1000 }
		]
	};

	$: livecode = `    
    const addSnack:any =getContext('addSnack')
    
    const snacktime = () => {    
      addSnack({
        message: 'I am a snackbar!', 
        type: 'primary', 
        duration: 4000, 
        closeOnClick: true,
      })
    }

    <Button exactfit type='primary' onClick={() => {snacktime()}}>Add Snack</Button>
     `;

	const addSnack: any = getContext('addSnack');

	const snacktime = () => {
		console.log(props);
		addSnack({
			message: 'I am a snackbar!',
			...props,
			...selectprops,
			...inputprops
		});
	};

	const withLink = () => {
		addSnack({
			component: Link,
			props: {
				text: "I'm a link component",
				href: '#library?component=snackbar&link=clicked',
				type: props.type,
				active: true
			},
			...props,
			...selectprops,
			...inputprops
		});
	};

	const withButton = () => {
		addSnack({
			component: Button,
			props: {
				text: "I'm a button component - click me!",
				type: props.type,
				exactfit: true,
				onClick: () => {
					alert('do something...');
				}
			},
			...props,
			...selectprops,
			...inputprops
		});
	};

	const noDuration = () => {
		const _selectprops = { ...selectprops };
		delete _selectprops.duration;

		addSnack({
			component: Link,
			props: {
				text: "I'm a link component",
				href: '#library?component=snackbar&link=clicked',
				type: props.type,
				active: true
			},
			...props,
			..._selectprops
		});
	};
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
		<Button
			exactfit
			applyTheme="primary"
			onClick={() => {
				snacktime();
			}}>Add Snack</Button
		>
		<Button
			exactfit
			applyTheme="secondary"
			onClick={() => {
				noDuration();
			}}>No Duration Snack</Button
		>
		<Button
			exactfit
			applyTheme="success"
			onClick={() => {
				withLink();
			}}>Add Snack (with link)</Button
		>
		<Button
			exactfit
			applyTheme="warning"
			onClick={() => {
				withButton();
			}}>Add Snack (with component)</Button
		>
	</div>
</LibrarySnippet>
