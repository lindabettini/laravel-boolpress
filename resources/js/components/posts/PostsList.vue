<template>
    <section id="post-list" class="my-3">
        <h2>Posts</h2>
        <Loader v-if="isLoading" />
        <ul v-if="posts.length">
            <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
        </ul>
        <p v-else>Non ci sono post</p>
    </section>
</template>

<script>
import Loader from "../Loader.vue";
export default {
    name: "PostsList",
    components: {
        Loader,
    },
    data() {
        return {
            posts: [],
            isLoading: false,
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
