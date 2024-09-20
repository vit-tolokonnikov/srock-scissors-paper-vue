<template>
    <TheHeader :title="title" />
    <main class="container">
        <div>Result: {{ resultText }}</div>
        <div>Score: {{ userScore }}:{{ computerScore }}</div>
        <div class="elem-container">
            <div
                v-for="elem in elems" :key="elem.id"
                @click="makeChoice(elem.name)" :class="['elem', elem.class]"
            ></div>
        </div>
    </main>
    <TheFooter/>
</template>

<script>
import TheHeader from "@/components/TheHeader.vue";
import TheFooter from "@/components/TheFooter.vue";

export default {
    name: 'App',
    components: {
        TheHeader,
        TheFooter,
    },
    data() {
        return {
            title: 'Rock Scissors Paper Vue',
            variants: ['rock', 'scissors', 'paper'],
            elems: [
                {
                    id: 0,
                    class: 'rock',
                    name: 'rock'
                },
                {
                    id: 1,
                    class: 'scissors',
                    name: 'scissors'
                },
                {
                    id: 2,
                    class: 'paper',
                    name: 'paper'
                },
            ],
            userScore: 0,
            computerScore: 0,
            resultText: ''
        };
    },
    methods: {
        makeChoice(elem) {
            const computerChoice = this.getComputerChoice();

            const rules = {
                rock: 'scissors',
                scissors: 'paper',
                paper: 'rock'
            };

            if (computerChoice === elem) {
                this.resultText = 'Draw';
            } else if (rules[elem] === computerChoice) {
                this.increaseUserScore();
            } else {
                this.increaseComputerScore();
            }
        },
        getComputerChoice() {
            const randomIndex = Math.floor(Math.random() * this.variants.length);

            return this.variants[randomIndex];
        },
        increaseUserScore() {
            this.userScore = this.userScore + 1;
            this.resultText = 'Win';
        },
        increaseComputerScore() {
            this.computerScore = this.computerScore + 1;
            this.resultText = 'Loss';
        }

    }
};
</script>

<style scoped>
.container {
    width: 900px;
    padding: 0 40px;
    margin: 0 auto;
}

.elem-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
}

.elem {
    width: 150px;
    height: 150px;
}

.rock {
    background: url("./assets/img/rock-empty.png");
}

.rock:hover {
    background: url("./assets/img/rock-full.png");
}

.scissors {
    background: url("./assets/img/scissors-empty.png");
}

.scissors:hover {
    background: url("./assets/img/scissors-full.png");
}

.paper {
    background: url("./assets/img/paper-empty.png");
}

.paper:hover {
    background: url("./assets/img/paper-full.png");
}
</style>