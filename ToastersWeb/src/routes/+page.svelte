<script>
    import NavBar from "$lib/allsites/NavBar.svelte";
    import ThemeBackground from "$lib/allsites/ThemeBackground.svelte";
    import GlowingBox from "$lib/goodies/GlowingBox.svelte";

    const text = ("This is just a test \n" +
        "to see how well the glowing \n" +
        "box component works. \n").replace(/\n/g, "<br>");


</script>

<ThemeBackground/>
<NavBar/>

<GlowingBox text={text} top="200px" right="160px"/>
