<template>
    <div id="playlistManager">
        <h1 class="title">Playlist Manager</h1>
        <section>
            <songlist :songs="songs" @add="moveToPlaylist" @addNewSong="addNewSong"></songlist>
            <playlist :songs="playlistSongs" @remove="moveToSonglist"></playlist>
        </section>
    </div>
</template>

<script>
import Playlist from './Playlist';
import Songlist from './Songlist';

export default {
    name: 'PlaylistManager',
    components: { Playlist, Songlist },
    data() {
        return {
            playlistSongs: [],  // this array will hold on to songs that have been added to the playlist
            songs: [
                { artist: 'Procol Harem', title: 'Whiter Shade of Pale' },
                { artist: 'Moody Blues', title: 'Night in White Satin' },
                { artist: 'Booker T & the MGs', title: 'Time is Tight' },
                { artist: 'Mark Knopler', title: 'Going Home' },
                { artist: 'Peter Gabriel', title: 'Don\'t Give Up' },
                { artist: 'Santana', title: 'Samba Pa Ti' },
                { artist: 'Edith Piaf', title: 'La Vie En Rose' },
                { artist: 'John Waite', title: 'Restless Heart' }
            ]
        }
    },
    methods: {
        addNewSong(song) {
            this.songs.splice(0, 0, song);
        },
        moveToPlaylist(index) {
            // splice the song out of songs and in to playlistSongs
            let song = this.songs.splice(index, 1)[0];
            this.playlistSongs.splice(0, 0, song);
        },
        moveToSonglist(index) {
            // splice the song out of playlistSongs and in to songs
            let song = this.playlistSongs.splice(index, 1)[0];
            this.songs.splice(0, 0, song);
        }
    }
}
</script>

<style scoped>
#playlistManager > section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 1rem;
    padding: 1rem;
}
</style>