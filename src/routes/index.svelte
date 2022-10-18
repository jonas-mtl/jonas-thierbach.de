<script>
    import "$lib/components/home/index.scss"

    import { onMount } from 'svelte';
    import { currentURL } from './stores/urlStore'
    import { fade, fly } from 'svelte/transition';


    let sliderValues = {s1: 1, s2: 0, s3: 0, s4:0}

    function delay(time) {
        return new Promise(resolve => setTimeout(resolve, time));
    }

    async function slideshow() {
        if (sliderValues.s1 === 1) {
            sliderValues.s2 = 1
            await delay(1000)
            sliderValues.s1 = 0
        }
        else if (sliderValues.s2 === 1) {
            sliderValues.s3 = 1
            await delay(1000)
            sliderValues.s2 = 0
        }
        else if (sliderValues.s3 === 1) {
            sliderValues.s4 = 1
            await delay(1000)
            sliderValues.s3 = 0
        }
        else {
            sliderValues.s1 = 1
            await delay(1000)
            sliderValues.s4 = 0
        }
    }

    onMount(() => {
        currentURL.set(window.location.href)
        setInterval(slideshow, 5000);
    });
</script>


<div in:fade="{{ duration: 400, delay: 410 }}" out:fade="{{ duration: 400 }}" class="index-main" style="font-family: 'Poppins', sans-serif;" >
    <div class="slide-containder">
        <div class="content">
            <div class="principal">
            </div>
        </div> 
        <div class="slider s1" style="opacity: {sliderValues.s1};"></div>
        <div class="slider s2" style="opacity: {sliderValues.s2};"></div>
        <div class="slider s3" style="opacity: {sliderValues.s3};"></div>
        <div class="slider s4" style="opacity: {sliderValues.s4};"></div>
    </div>
</div>