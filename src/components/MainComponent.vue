<template>
    <div class="container">
        <div class="row">
            <div class="question-box col-md-12 m-auto">
                <h1>The Quiz</h1>
                <section class="quiz" v-if="!quizCompleted">
                    <div class="quiz-info">
                        <span class="question">{{
                            getCurrentQuestion.question
                        }}</span>
                    </div>
                    <div class="options">
                        <label
                            v-for="(
                                option, index
                            ) in getCurrentQuestion.options"
                            :key="index"
                            :class="`option ${
                                getCurrentQuestion.selected == index
                                    ? index == getCurrentQuestion.answer
                                        ? 'correct'
                                        : 'wrong'
                                    : ''
                            } ${
                                getCurrentQuestion.selected != null &&
                                index != getCurrentQuestion.selected
                                    ? ' disabled'
                                    : ''
                            }`"
                        >
                            <input
                                type="radio"
                                :name="getCurrentQuestion.index"
                                :value="index"
                                v-model="getCurrentQuestion.selected"
                                :disabled="getCurrentQuestion.selected"
                                @change="SetAnswer"
                            />
                            <span>{{ option }}</span>
                        </label>
                    </div>
                    <button
                        class="mt-4 btn btn-primary"
                        @click="nextQuestion"
                        :disabled="getCurrentQuestion.selected === null"
                    >
                        {{
                            getCurrentQuestion.index === questions.length - 1
                                ? "Finish"
                                : getCurrentQuestion.selected == null
                                ? "Select an option"
                                : "Next question"
                        }}
                    </button>
                </section>

                <section v-else>
                    <h2>You have finished the quiz.</h2>
                    <p>Your score is {{ score }} / {{ questions.length }}</p>
                </section>
            </div>
        </div>
    </div>
</template>

<script>
import { ref, computed } from "vue";
import { useRouter, useRoute } from "vue-router";

export default {
    setup() {
        const router = useRouter();
        const route = useRoute();

        const questions = ref([
            {
                question: "What is Vue Js?",
                answer: 0,
                options: ["A Framework", "A Library", "A Language"],
                selected: null,
            },
            {
                question: "What is Vuex?",
                answer: 2,
                options: [
                    "Vue with x",
                    "A Library",
                    "A State Management library",
                ],
                selected: null,
            },
            {
                question: "What is Vue Router used for?",
                answer: 1,
                options: [
                    "Vue with x",
                    "A routing library for Vue Js",
                    "A State Management library",
                ],
                selected: null,
            },
        ]);

        const quizCompleted = ref(false);
        const currentQuestion = ref(0);
        const score = computed(() => {
            let value = 0;
            questions.value.map((question) => {
                if (question.selected == question.answer) {
                    value++;
                }
            });
            return value;
        });
        const getCurrentQuestion = computed(() => {
            let question = questions.value[currentQuestion.value];
            question.index = currentQuestion.value;
            return question;
        });

        const SetAnswer = (event) => {
            questions.value[currentQuestion.value].selected =
                event.target.value;
            event.target.value = null;
        };

        const nextQuestion = () => {
            if (currentQuestion.value < questions.value.length - 1) {
                currentQuestion.value++;
            } else {
                quizCompleted.value = true;
            }
        };

        return {
            questions,
            quizCompleted,
            currentQuestion,
            score,
            getCurrentQuestion,
            SetAnswer,
            nextQuestion,
        };
    },
};
</script>

<style lang="scss">
.btn {
    margin: 10px;
    background-color: rebeccapurple;
    border-radius: 10px;
    color: blanchedalmond;
    appearance: none;
    outline: none;
    border: none;

    &:hover {
        background-color: #2c0dc5a3;
    }
}
.question-box {
    background-color: #271c36;
    border-radius: 10px;
    padding: 10px;
    margin: 10px;
    border: 1px solid #2c3e50;
    .options {
        margin: 15px auto auto auto;
    }
    .option {
        width: 50%;
        height: 80px;
        background-color: #18b7d6;
        border-radius: 10px;
        padding: 10px;
        margin: 15px auto auto auto;
        display: flex;
        justify-content: center;
        align-items: center;
        &:hover {
            background-color: #bd348d2e;
            color: #18b7d6;
            cursor: pointer;
        }

        &:last-of-type {
            margin-bottom: 0;
        }
        &.wrong {
            background-color: #d72332;
        }
        &.correct {
            background-color: #1ed618;
        }
        &.disabled {
            opacity: 0.5;
        }
    }

    input {
        display: none;
    }
}

h1,
p {
    color: #18b7d6;
}
</style>
