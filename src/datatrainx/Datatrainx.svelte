<script>

    import {fly } from 'svelte/transition';
    import Presentation from "./Presentation.svelte";
    import Cnn from './Cnn.svelte';
    import Article from "./article/Article.svelte";
    import Layout from "./layout/Layout.svelte";
    import Start from "./trainx/Start.svelte";
    import ResultatKolb from "./resultat/ResultatKolb.svelte";
    import OpenData from "./OpenData.svelte";
    import Calculs from "./utils/Calculs.svelte";
    import Test from "./trainx/DebugTest.svelte";

    import {chartStore, layoutStore, userIdtStore, videoStore} from "../stores";

    //Layout DataTrainX presentation
    export const views = {
        presentation: Presentation,
        cnn: Cnn,
        start: Start,
        opendata:OpenData,
        resultatKolb:ResultatKolb,
        calculs:Calculs,
        test:Test
    };

    let layoutValue;
    let playVideo;
    let playChart;
    let viewportComponent = null;

    layoutStore.subscribe(value => {
        layoutValue = value;
    });
    videoStore.subscribe(value => {
        playVideo = value;
    });
    chartStore.subscribe(value => {
        playChart = value;
    });
    function updateViewportComponent() {
        videoStore.set(false);
        if (typeof playChart.destroy === "function") {
            playChart.destroy();
        }
        viewportComponent = views[layoutValue];
    }
    updateViewportComponent();
</script>

<style>
#main{
    padding: 1em;
    background-color: #3b065e;
}

@media only screen and (max-width: 600px) {
    #main{
        padding: 1em 0;
        background-color: #3b065e;
    }
}

</style>
<main>
    {#if viewportComponent == views[layoutValue]}
    <section id='main' class="hero is-fullheight" on:outroend={updateViewportComponent} transition:fly="{{ y: 200, duration: 1000 }}">
        <Layout>
            <svelte:component this={viewportComponent}/>
        </Layout>
    </section>
    {/if}

    <section id='article' class="section">
        <Article/>
    </section>
</main>