<script setup>

// Créer des thumbnail vide ici

import { ref, onMounted } from 'vue';
import { RouterLink } from 'vue-router';

// Appel a l'api

const playlists = ref(null)

onMounted(async () => {
    const values = await fetch("http://46.101.222.19:4000/api/playlists/top/15")
    const jsonValues = await values.json()
    playlists.value = jsonValues["data"]
    console.log("playlists", playlists.value)
})

</script>


<template>
    <div class="home">
        <h1>
            Playlists
        </h1>
        <div class="playlists">
            <div v-for="playlist in playlists">
                <div class="playlist-item">
                    <router-link :to="{ name: 'playlist', params: { id: playlist.id } }"><img
                            :src="playlist.picture_medium" /></router-link>
                    <b>{{ playlist.title }}</b>
                    <span>{{ playlist.user.name }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
h1 {
    font-size: small;
}

.home {
    overflow-y: scroll;
}

.playlists {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
}


.playlist-item {
    display: flex;
    flex-direction: column;
    width: 150px;
    height: 250px;
    margin: 10px;
}


.playlist-item img {
    width: 100%;
    height: auto;
}

@media (min-width: 1024px) {

    h1 {
        font-size: 2em;
    }

    .playlist-item {
        display: flex;
        flex-direction: column;
        width: 200px;
        height: 300px;
        margin: 15px;
    }

}
</style>