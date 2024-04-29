<script>
    import ThemeBackground from "$lib/allsites/ThemeBackground.svelte";
    import NavBar from "$lib/allsites/NavBar.svelte";
    import GlowingBox from "$lib/goodies/GlowingBox.svelte";

    const aboutMinecraft = ("This page will store all the information \n" +
        "relevant to the minecraft servers, plugins, and libraries.\n" +
        "The server aims to be a RPG based server with lots of things to " +
        "do. \n"
    ).replace(/\n/g, "<br>");

		const aboutWonderland = ("Wonderland is a project that aims to bring more ease of use into development. \n" +
				"Wonderland comes with a set of tools to help move along production faster. \n"
		)
		const hoverWonderland = "As of 4/29/24 Wonderland is going through a rewrite to be more java friendly, " +
			"and for a few other improvements on how I did things."

		const aboutToasters =("Toasters is an RPG plugin for the Toasters Minecraft server. The plugin is built by Toast alongside Faceless. \n" +
				"Toasters is built with the Wonderland library, and a mix of both Java and Kotlin. Little war between languages we got going on. "
		)
		const hoverToasters = "ToastersRPG is still undergoing some development. " +
			"The download will give you a zip of our latest published works to our github."

		let wonderlandVersion = "v1.0.8"
		let wonderland = "https://github.com/ToastArgumentative/ToastWonderland/archive/refs/tags/ALPHA-1.0.8.zip"
		let wonderlandRepo = "https://github.com/ToastArgumentative/ToastWonderland"

		let toastersVersion = "v1.0.0"
		let toastersrpg = "https://github.com/ToastArgumentative/ToastersRPG/archive/refs/heads/master.zip"
		let toastersRepo = "https://github.com/ToastArgumentative/ToastersRPG"

</script>

<ThemeBackground/>
<NavBar/>

<GlowingBox text={aboutMinecraft} title="Welcome!"
						top="75px" right="500px"
						showFullText=true
/>

<GlowingBox text={aboutWonderland}
						title="Wonderland: {wonderlandVersion}"
						hoverText={hoverWonderland}
						titleLink={wonderlandRepo}

						top="335px" left="75px"
						downloadLink={wonderland}

/>

<GlowingBox text={aboutToasters} title="ToastersRPG: {toastersVersion}" hoverText={hoverToasters}
						top="335px" right="75px"
						downloadLink={toastersrpg}
						downloadGoodOrBad="bad"

/>