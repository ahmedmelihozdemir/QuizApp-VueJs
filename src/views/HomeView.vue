<template>
    <div class="home">
        <h1>Welcome to Quizze App</h1>
        <p>Test your general knowledge with 10 questions</p>
        <button @click="start" class="btn btn-primary">Start Quiz</button>
    </div>
</template>

<script lang="ts">
import { ref } from "vue";
import { useRouter, useRoute } from "vue-router";

export default {
    setup() {
        const router = useRouter();
        const route = useRoute();

        const start = ref(() => {
            router.push("/quiz");
        });

        return {
            start,
        };
    },
};
</script>
