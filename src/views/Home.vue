<template>
    <div class="wrapper">
        <form class="searchbar text-centered">
            <label>
                <span class='screen-reader-only'>Search:</span>
                <input
                    v-model="tag"
                    placeholder="Search for location"
                    type="text"
                    class="searchbar-input">
            </label>
            <button
                type="submit"
                class="btn btn--green btn--go"
                @click.prevent="search">
                Go
            </button>
        </form>
        <p v-if="loading" class="text-centered">
            Loading...
        </p>
        <ul v-else class="image-card-grid">
            <image-card
            v-for="image in images"
            :key="image.id"
            :image="image" />
        </ul>
    </div>
</template>

<script>
    import flickr from '../flickr.js';
    import ImageCard from '@/components/ImageCard';

    export default {
        name: 'home',
        components: {
            ImageCard,
        },
        data() {
            return {
                loading: false,
                tag: '',
                images: [],
            };
        },
        methods: {
            search() {
                this.loading = true;
                this.fetchImages();
                this.loading = false;
            },
            fetchImages() {
                return flickr('photos.search', {
                    tags: this.tag,
                    extras: 'url_n, owner_name, description, date_taken, views',
                    page: 1,
                    per_page: 30,
                }).then((response) => {
                    this.images = response.data.photos.photo
                });
            },
        },
    };
</script>

<style lang="scss">
    .screen-reader-only {
        height: 1px;
        width: 1px;
        position: absolute;
        left: -100000px;
    }
    .text-centered {
        text-align: center;
    }
    .wrapper {
        margin: 0 auto;
        max-width: 800px;
        @media only screen and (max-width: 799px) {
            max-width: 100%;
            margin: 0 1.5rem;
        }
    }
    .image-card-grid {
        list-style: none;
        margin: .5rem 0;
        padding: 0;
        display: flex;
        align-items: flex-start;
        flex-wrap: wrap;
    }
    .searchbar {
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        @media only screen and (max-width: 549px) {
            width: 100%;
            label {
                width: 80%;
            }
        }
    }
    .searchbar-input {
        padding: .5rem 1rem;
        border-radius: 20px;
        font-size: 1rem;
        border: 1px solid gray;
        min-width: 300px;
        @media only screen and (max-width: 549px) {
            min-width: 0;
            width: 100%;
        }
    }
    .btn {
        padding: .5rem 1rem;
        font-size: 1rem;
        border-radius: 20px;
        background: transparent;
        border: none;
    }
    .btn--green {
        background: #42b983;
        color: white;
        font-weight: bold;
    }
    .btn--go {
        padding: .5rem 2rem;
        margin-left: 1rem;
    }
</style>
