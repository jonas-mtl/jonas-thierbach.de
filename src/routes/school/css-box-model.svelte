<script>
    import "$lib/components/school/projects/css-box-model.scss"
    import { fade, fly, scale } from 'svelte/transition';
    import { cubicInOut } from 'svelte/easing';

    function switchTab(tabQuery) {
        if (tabQuery === 0) varName = "padding"
        else if (tabQuery === 1) varName = "margin"
        else varName = "border"

        activeTabPadding[tabQuery] = "active"
        
        activeTabPadding[tabQuery - 1] = "inactive"
        activeTabPadding[tabQuery - 2] = "inactive"
        activeTabPadding[tabQuery + 1] = "inactive"
        activeTabPadding[tabQuery + 2] = "inactive"
    }

    function setAlign(align) {
        outerFlexAlign = align
    }

    function setJustify(justify) {
        outerFlexJustify = justify
    }

    let activeTabPadding = ["active","inactive","inactive"]
    let varName = "padding"

    let h = 0
    let w = 0
    
    let top = 50;
    let right = 50;
    let bottom = 50;
    let left = 50;

    let outerFlexJustify = "left"
    let outerFlexAlign = "flex-start"

    let margintop = 50
    let marginright = 50
    let marginbottom = 50
    let marginleft = 50

    let bordertop = 5
    let borderright = 5
    let borderbottom = 5
    let borderleft = 5
</script>

<div class="main-box-model" style="font-family: 'Poppins', sans-serif;" in:fade="{{ duration: 400, delay: 420 }}" out:fade="{{ duration: 400 }}">
    <h1 in:fly="{{ y: 20, duration: 2000 }}">
        Das CSS Box-Modell
    </h1>
    <span class="border"   in:scale={{
		delay: 250,
		duration: 2000,
		baseScale: 0.5
	}}></span>
    <p in:fade="{{ duration: 2000, delay: 390 }}">
        Das CSS-Box-Modell ist im Wesentlichen eine Box, die jedes HTML-Element umschließt. <br> Es besteht aus: Margins, Borders, Padding und dem eigentlichen Inhalt:
    </p>
    <div class="wrapper">
        <div class="container-boxes" in:fly="{{ y: 100, duration: 2000 }}">
            <div class="outer-box" style="justify-content: {outerFlexJustify}; align-items: {outerFlexAlign}; width: {w}px; height: {h}px">
                <div class="inner-box" style="padding: {top / 4}% {right / 4}% {bottom / 4}% {left / 4}%; margin: {margintop / 4}% {marginright / 4}% {marginbottom / 4}% {marginleft / 4}%; border-top: {bordertop / 3}px solid rgb(187, 187, 187); border-right: {borderright / 3}px solid rgb(187, 187, 187); border-left: {borderleft / 3}px solid rgb(187, 187, 187); border-bottom: {borderbottom / 3}px solid rgb(187, 187, 187);">
                    <h3>Inhalt</h3>
                </div>
            </div>
        </div>
        <div class="container-slider" bind:clientWidth={w} bind:clientHeight={h}>
            <div class="tabs" style="user-select: none;" >
                <button on:click|preventDefault={() => switchTab(0)} class={activeTabPadding[0]}>Padding</button>
                <button on:click|preventDefault={() => switchTab(1)} class={activeTabPadding[1]}>Margin</button>
                <button on:click|preventDefault={() => switchTab(2)} class={activeTabPadding[2]}>Border</button>
            </div>
            <div class="Padding" in:fly="{{ y: 100, duration: 2000,delay: 100 }}">
                <div class="sliders">
                    <table style="user-select: none;">
                        {#if activeTabPadding[0] === "active"}
                            <tr>
                                <td>Oben</td>
                                <td><input type="range" id="top" bind:value={top}></td>
                            </tr>
                            <tr>
                                <td>Rechts</td>
                                <td><input type="range" id="top" bind:value={right}></td>
                            </tr>
                            <tr>
                                <td>Unten</td>
                                <td><input type="range" id="top" bind:value={bottom}></td>
                            </tr>
                            <tr>
                                <td>Links</td>
                                <td><input type="range" id="top" bind:value={left}></td>
                            </tr>
                        {:else if activeTabPadding[1] === "active"}
                            <tr>
                                <td>Oben</td>
                                <td><input type="range" id="top" bind:value={margintop} on:focus={() => setAlign("flex-start")}></td>
                            </tr>
                            <tr>
                                <td>Rechts</td>
                                <td><input type="range" id="top" bind:value={marginright} on:focus={() => setJustify("right")}></td>
                            </tr>
                            <tr>
                                <td>Unten</td>
                                <td><input type="range" id="top" bind:value={marginbottom} on:focus={() => setAlign("flex-end")}></td>
                            </tr>
                            <tr>
                                <td>Links</td>
                                <td><input type="range" id="top" bind:value={marginleft} on:focus={() => setJustify("left")}></td>
                            </tr>
                        {:else}
                            <tr>
                                <td>Oben</td>
                                <td><input type="range" id="top" bind:value={bordertop}></td>
                            </tr>
                            <tr>
                                <td>Rechts</td>
                                <td><input type="range" id="top" bind:value={borderright}></td>
                            </tr>
                            <tr>
                                <td>Unten</td>
                                <td><input type="range" id="top" bind:value={borderbottom}></td>
                            </tr>
                            <tr>
                                <td>Links</td>
                                <td><input type="range" id="top" bind:value={borderleft}></td>
                            </tr>
                        {/if}
                    </table>
                </div>
                <div class="code">
                    <pre data-language="css" style="background-color: #4e4331; color: #c9cdd7">
<code><span style="color: #8c836e">/* CSS Code: */</span>
<span style="color: #FF8383">.container &#123;</span>
<span style="color: #AFF19F">   {varName}: </span><span style="color: #D1D5DE">{activeTabPadding[0] === "active" ? top : activeTabPadding[1] === "active" ? margintop : bordertop}px {activeTabPadding[0] === "active" ? right : activeTabPadding[1] === "active" ? marginright : borderright}px {activeTabPadding[0] === "active" ? bottom : activeTabPadding[1] === "active" ? marginbottom : borderbottom}px {activeTabPadding[0] === "active" ? left : activeTabPadding[1] === "active" ? marginleft : borderleft}px</span><span style="color: #AFF19F">;</span>
<span style="color: #FF8383">}</span></code>
                    </pre>
                </div>

            </div>
        </div>
    </div>
</div>