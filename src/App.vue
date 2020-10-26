<template>
    <div id="app">
        <fu-header />
        <div class="app-podcasts" v-if="podcasts.length > 0">
            <div
                class="app-podcast"
                v-for="(podcast, index) in podcasts"
                :key="`podcast_${index}`"
                @click="handleClickPodcast(podcast)"
            >
                <fu-podcast
                    :image="podcast.urls.logo_image.original"
                    :name="podcast.title"
                    :active="comparePodcastWithCurrent(podcast)"
                />
            </div>
        </div>
        <div v-if="currentPodcastClips.length > 0" class="app-player">
            <fu-player
                :name="getFirstClip.title"
                :album="getFirstClip.channel.title"
                :url="getFirstClip.urls.high_mp3"
                :image="getFirstClip.channel.urls.logo_image.original"
            />
        </div>
    </div>
</template>

<script>
import FuPlayer from "./components/FuPlayer";
import FuHeader from "./components/FuHeader";
import FuPodcast from "./components/FuPodcast";
export default {
    name: "App",
    components: {
        FuPlayer,
        FuHeader,
        FuPodcast,
    },
    created() {
        fetch("https://api.audioboom.com/channels/recommended")
            .then((response) => response.json())
            .then((data) => {
                this.podcasts = data.body;
            });
    },
    data() {
        return {
            currentPodcastClips: [],
            podcasts: [],
            currentPodcast: null,
            paused: true,
        };
    },
    computed: {
        getFirstClip() {
            return this.currentPodcastClips[0];
        },
    },
    methods: {
        async handleClickPodcast(podcast) {
            const { id } = podcast;
            this.currentPodcast = podcast;

            const clips = await this.getAudioClips(id);
            this.currentPodcastClips = clips;
            console.log(this.currentPodcastClips);
        },
        getAudioClips(id) {
            return fetch(`https://api.audioboom.com/channels/${id}/audio_clips`)
                .then((response) => response.json())
                .then((data) => data.body.audio_clips);
        },
        comparePodcastWithCurrent(podcast) {
            if (this.currentPodcast) {
                return podcast.id === this.currentPodcast.id;
            }
            return false;
        },
    },
};
</script>

<style>
body {
    margin: 0px;
}
.app-podcast {
    margin-bottom: 37px;
    margin-left: 16px;
}
.app-podcasts {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    margin-top: 16px;
}

.app-player {
    position: fixed;
    bottom: 0;
    width: 100%;
}
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    margin: 0px;
}
</style>
