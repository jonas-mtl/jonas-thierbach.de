<script>
    import "$lib/components/school/school.scss"

    import { currentURL } from './stores/urlStore'
    import { fade, fly } from 'svelte/transition';
    import { onMount } from 'svelte';


    onMount(() => {
        currentURL.set(window.location.href)
	});
</script>

<main style="font-family: 'Poppins', sans-serif;" in:fade="{{ duration: 400, delay: 410 }}" out:fade="{{ duration: 400 }}">
    <div class="container">
        <span>
            <h1 in:fly="{{ y: 20, duration: 2000 }}">
                Schulprojekte
            </h1>
        </span>
        <div class="entrys">
            <section id="archive">
                <div class="div">
                    <h3 in:fade={{duration: 1000}}>2022</h3>
                    <ul>
                        <li><a href="/school/css-box-model">CSS Box-Modell interaktiv dargestellt (margin, padding, border) / Informatik 05.10.2022</a></li>
                        <li><a href="/">Erstellung jonas-thierbach.de eigene Webseite & Portfolio / 21.09.2022</a></li>

                    </ul>
                </div>
            </section>
        </div>
    </div>
</main>