<template lang="html">
    <div class="fu-player">
        <img class="fu-player_image" :src="image" :alt="name" />
        <div class="fu-player_details">
            <p class="fu-player_name">{{ name }}</p>
            <p class="fu-player_album">{{ album }}</p>
        </div>
        <div class="fu-player_play" v-on:click="handlePodcast">
            <i v-show="isPaused" class="fas fa-play"></i>
            <i v-show="!isPaused" class="fas fa-pause"></i>
        </div>
        <div class="fu-player_volume">
            <input
                type="range"
                class="fu-player_volumeRange"
                min="0"
                max="100"
                v-model="volume"
                v-on:input="setVolume"
            />
            <div class="fu-player_volumeIcon" v-on:click="toogleVolume">
                <i v-show="volume > 0" class="fas fa-volume-up"></i>
                <i v-show="volume == 0" class="fas fa-volume-mute"></i>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "FuPlayer",
    props: {
        name: {
            type: String,
            required: true,
        },
        album: {
            type: String,
            required: true,
        },
        url: {
            type: String,
            required: true,
        },
        image: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            isPaused: true,
            volume: 50,
        };
    },
    computed: {
        audio() {
            return new Audio(this.url);
        },
    },
    methods: {
        handlePodcast() {
            if (this.audio.paused) {
                this.audio.play();
                this.isPaused = false;
            } else {
                this.audio.pause();
                this.isPaused = true;
            }
        },
        setVolume() {
            this.audio.volume = this.volume / 100;
        },
        toogleVolume() {
            if (this.audio.muted) {
                this.volume = 100;
                this.audio.muted = false;
            } else {
                this.volume = 0;
                this.audio.muted = true;
            }
            this.setVolume();
        },
    },
};
</script>

<style lang="css" scoped>
.fu-player {
    display: grid;
    grid-template-columns: 100px repeat(3, 1fr);
    background: #2196f3;
    width: 100%;
    height: 100px;
}
.fu-player_image {
    width: 100px;
    height: 100px;
    object-fit: cover;
    vertical-align: top;
}
.fu-player_details {
    margin-left: 20px;
    color: #fff;
    align-self: center;
}
.fu-player_name {
    font-weight: bold;
    font-size: 14px;
    font-family: Quicksand;
}
.fu-player_album {
    font-weight: 400;
    font-size: 12px;
    font-family: Quicksand;
}
.fu-player_play {
    align-self: center;
    justify-self: center;
    color: white;
    font-size: 20px;
    background: #6abdff;
    height: 60px;
    width: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    cursor: pointer;
}
.fu-player_previus {
    align-self: center;
    justify-self: center;
    color: white;
    font-size: 20px;
    background: #6abdff;
    height: 60px;
    width: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    cursor: pointer;
}
.fu-player_next {
    align-self: center;
    justify-self: center;
    color: white;
    font-size: 20px;
    background: #6abdff;
    height: 60px;
    width: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    cursor: pointer;
}

.fu-player_volume {
    justify-self: end;
    display: flex;
    align-items: center;
    margin-right: 32px;
}
.fu-player_volumeRange {
    appearance: none;
    outline: none;
    height: 6px;
    border-radius: 8px;
    cursor: pointer;
}
.fu-player_volumeIcon {
    color: #fff;
    font-size: 20px;
    margin-left: 40px;
    cursor: pointer;
}
</style>
