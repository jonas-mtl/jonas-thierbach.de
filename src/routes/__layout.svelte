<script>
    import "$lib/components/global/header.scss"

    import FaHome from 'svelte-icons/fa/FaHome.svelte';
	import FaBook from 'svelte-icons/fa/FaBook.svelte';
	import FaDove from 'svelte-icons/fa/FaDove.svelte';
	import FaEnvelopeOpenText from 'svelte-icons/fa/FaEnvelopeOpenText.svelte';
    import { currentURL } from './stores/urlStore'

    let homeStatus = false
    let url = '';
    $: {
        setNavClosed(url)
    }
    let mobileMenuStatus = false;
    let y
    $: {
        setNavClosed(y)
    }

    currentURL.subscribe(value => {
		url = value;
	});

    function setNavClosed(y) {
        mobileMenuStatus = false
        return y;
    }

    function menuTriggered() {
        mobileMenuStatus = !mobileMenuStatus
    }

</script>

<svelte:window bind:scrollY={y} />

<header style="font-family: 'Poppins', sans-serif;">
    <div class="cnt" style="background-color: {homeStatus ? "none" : "#eeeae5"}; backdrop-filter: blur({homeStatus ? "60" : "0"}px);">
       <a href="/"><div class="wrapper">
            <img src="/images/leaf.png" alt="logoSm" class="logoSm">
            <h1>Jonas</h1><h2> Thierbach</h2>
        </div></a>

        <nav>
            <a href="/">Home</a>
            <a href="/archive">Projekte</a>
            <a href="/school">Schule</a>
            <a href="/about">Über</a>
        </nav>

        <div class="mobileWrapper">
            <div on:click={() => menuTriggered()} class="burgerMenu">
                <div class={`column ${ mobileMenuStatus && 'menuActive'}`}></div>
                <div class={`column ${ mobileMenuStatus && 'menuActive'}`}></div>
                <div class={`column ${ mobileMenuStatus && 'menuActive'}`}></div>
            </div>
            
        </div>
    </div>
</header>
<div class={ mobileMenuStatus === true ? 'blur active' : 'blur closed'}></div>
<nav class={ mobileMenuStatus === true ? 'mobileNav active' : 'mobileNav closed'}>
    <div class="text-container-nav">
        <ul>
            <a href="/"><li class={ url.endsWith('/') && 'activeTab'}> Home <span id="icon"><FaHome /></span></li></a>
            <a href="/archive"><li class={ url.endsWith('/archive') && 'activeTab'}> Projekte <span id="icon"><FaBook class="icon"/></span></li></a>
            <a href="/school"><li class={ url.endsWith('/school') && 'activeTab'}> Schule <span id="icon"><FaDove class="icon"/></span></li></a>
            <a href="/about"><li class={ url.endsWith('/about') && 'activeTab'}> Über <span id="icon"><FaEnvelopeOpenText class="icon"/></span></li></a>
        </ul>
    </div>
</nav>

<slot />