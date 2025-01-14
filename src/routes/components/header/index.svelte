<script lang="ts">
	import LibrarySnippet from '@component/base/LibrarySnippet.svelte';

	import Header from '@layout/Header.svelte';
	import NavBar from '@layout/NavBar.svelte';
	import HeroBanner from '@layout/HeroBanner.svelte';
	import ThemeSwitch from '@utility/ThemeSwitch.svelte';
	import Search from '@layout/Search.svelte';

	import { svgslist } from '@text/SVG.svelte';

	let propstr = '';
	let selectstr = '';
	let inputstr = '';
	let props;
	let selectprops;
	let inputprops;

	const snippet = {
		name: 'Header',
		importName: '@layout/Header.svelte',
		props: {
			showBurgerMenuButton: true,
			invertTheme: false,
			showHero: true,
			showFooter: true,
			showNotch: true,
			hideTitle: false,
			hideLogo: false,
			hideNav: false
		},
		dropdowns: [
			{
				label: 'notchOpenIcon',
				options: [...svgslist],
				value: 0
			},
			{
				label: 'notchCloseIcon',
				options: [...svgslist],
				value: 7
			}
		],
		inputs: [
			{ forprop: 'title', renderAs: 'input', componentprop: { type: 'text' }, value: 'MySite' },
			{ forprop: 'version', renderAs: 'input', componentprop: { type: 'text' }, value: '0.1.1' },
			{
				forprop: 'logoSrc',
				renderAs: 'input',
				componentprop: { type: 'text' },
				value: 'https://picsum.photos/id/10/20/20'
			},
			{
				forprop: 'bgSrc',
				renderAs: 'input',
				componentprop: { type: 'text' },
				value: 'https://picsum.photos/id/10/1440/600'
			}
		]
	};

	let staticprops = {
		navEle: {
			component: NavBar,
			props: {
				links: [
					{
						title: 'Home',
						icon: 'icon',
						href: '#components?component=header&link=home',
						active: true
					},
					{
						title: 'About',
						icon: 'icon',
						href: '#components?component=header&link=about',
						active: false
					},
					{
						title: 'Contact',
						icon: 'icon',
						href: '#components?component=header&link=contact',
						active: false
					}
				]
			}
		},
		heroEle: {
			component: HeroBanner,
			props: {
				title: 'MySite',
				buttonOne: {
					text: 'Info',
					applyTheme: 'black',
					href: '#components?component=header&link=cta1',
					size: 'large',
					rounded: true
				},
				buttonTwo: {
					text: 'Purchase',
					applyTheme: 'primary',
					href: '#components?component=header&link=cta2',
					size: 'large',
					hollow: false,
					rounded: true
				}
			}
		},
		footerEle: {
			component: ThemeSwitch
		},
		notchEle: {
			component: Search,
			show: true
		}
	};

	$: livecode = ` 
    import NavBar from '@layout/NavBar.svelte'
    import HeroBanner from '@layout/HeroBanner.svelte'
    import ThemeSwitch from '@utility/ThemeSwitch.svelte';
    import Search from '@layout/Search.svelte'

    let headerprops = {
      navEle: {
        component: NavBar,
        props: {
          links: [
            {title: 'Home', icon: 'icon', href: '#components?component=header&link=home', active: true},
            {title: 'About', icon: 'icon', href: '#components?component=header&link=about', active: false},
            {title: 'Contact', icon: 'icon', href: '#components?component=header&link=contact', active: false}
          ]
        }
      },
      heroEle: {
        component: HeroBanner,
        props: {
          buttonOne: {
            text: 'Info',
            type: 'hollow',
            applyTheme: 'black',
            href: '#components?component=header&link=cta1',
            size: 'large',
            rounded: true,     
          },
          buttonTwo: {
            text: 'Purchase',
            applyTheme: 'white',
            href: '#components?component=header&link=cta2',
            size: 'large',
            hollow: true,
            rounded: true,          
          }        
        }
      },
      footerEle: {
        component: ThemeSwitch
      },
      notchEle:  {
        component: Search,
        show: true,
      }     
    }
      
    <Header {...headerprops} ${propstr}${selectstr}${inputstr}/> 
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
		<Header {...staticprops} {...props} {...selectprops} {...inputprops} />
	</div>
</LibrarySnippet>
