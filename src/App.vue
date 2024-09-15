<template>
    <header class="container">
        <h1>{{ title }}</h1>
    </header>
    <main class="container">
        <div>Result: {{ resultText }}</div>
        <div>Score: {{ userScore }}:{{ computerScore }}</div>
        <div class="elem-container">
            <div @click="makeChoice('rock')" class="elem rock"></div>
            <div @click="makeChoice('scissors')" class="elem scissors"></div>
            <div @click="makeChoice('paper')" class="elem paper"></div>
        </div>
    </main>
    <footer>

    </footer>
</template>

<script>
export default {
    name: 'App',
    data() {
        return {
            title: 'Rock Scissors Paper Vue',
            variants: ['rock', 'scissors', 'paper'],
            userScore: 0,
            computerScore: 0,
            resultText: ''
        };
    },
    methods: {
        makeChoice(elem) {
            const computerChoice = this.getComputerChoice();
            console.log(elem)
            if (computerChoice === elem) {
                this.resultText = 'Draw'
            } else if (computerChoice === 'rock' && elem === 'scissors') {
                this.increaseComputerScore();
            } else if (computerChoice === 'rock' && elem === 'paper') {
                this.increaseUserScore();
            } else if (computerChoice === 'scissors' && elem === 'paper') {
                this.increaseComputerScore();
            } else if (computerChoice === 'scissors' && elem === 'rock') {
                this.increaseUserScore();
            } else if (computerChoice === 'paper' && elem === 'scissors') {
                this.increaseUserScore();
            } else if (computerChoice === 'paper' && elem === 'rock') {
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