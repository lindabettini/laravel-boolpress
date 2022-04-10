<template>
    <section id="post-list" class="my-3">
        <h2>Posts</h2>
        <Loader v-if="isLoading" />

        <div v-else>
            <div
                class="alert alert-danger d-flex justify-content-between"
                role="alert"
                v-if="hasError"
            >
                Si è verificato un errore!
                <span role="button" @click="hasError = !hasError">&times;</span>
            </div>

            <ul v-if="posts.length">
                <PostCard v-for="post in posts" :key="post.id" :post="post" />
            </ul>
            <p v-else>Non ci sono post</p>
        </div>
    </section>
</template>

<script>
import Loader from "../Loader.vue";
import PostCard from "./PostCard.vue";

export default {
    name: "PostsList",
    components: {
        Loader,
        PostCard,
    },
    data() {
        return {
            posts: [],
            isLoading: false,
            hasError: false,
        };
    },
    methods: {
        getPosts() {
            this.isLoading = true;
            axios
                .get("http://localhost:8000/api/posts")
                .then((res) => {
                    this.posts = res.data;
                })
                .catch((err) => {
                    console.error(err);
                    this.hasError = true;
                })
                .then(() => {
                    this.isLoading = false;
                    console.log("chiamata terminata");
                });
        },
    },
    mounted() {
        this.getPosts();
    },
};
</script>

<style></style>
