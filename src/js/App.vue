<template>
    <div>

        <div class="view-form" v-if="form">
            <div class="columns">
                <div class="column">
                    <form action="">
                        <div class="field">
                            <label class="label" for="background">Background</label>
                            <div class="control">
                                <div class="select">
                                    <select name="background" id="background" v-model="background" @change="updateValues">
                                        <option v-for="(name, key) in factions" v-bind:value="key">{{ name }}</option>
                                    </select>
                                </div>
                            </div>
                        </div>
                        <div class="field">
                            <label for="tournament" class="label">Tournament</label>
                            <div class="control">
                                <input type="text" v-model="tournament" id="tournament" placeholder="tournament"
                                       class="input" @keyup="updateValues"/>
                            </div>
                        </div>
                        <div class="columns">
                            <div class="column is-two-thirds">
                                <div class="field">
                                    <label for="player1" class="label">Player 1</label>
                                    <div class="control">
                                        <input type="text" v-model="player1" id="player1" placeholder="Player 1"
                                               class="input" @keyup="updateValues"/>
                                    </div>
                                </div>
                            </div>
                            <div class="column">
                                <div class="field">
                                    <label for="score1" class="label">Score 1</label>
                                    <div class="control">
                                        <input type="number" v-model="score1" id="score1" placeholder="0"
                                               class="input" @keyup="updateValues"/>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="columns">
                            <div class="column is-two-thirds">
                                <div class="field">
                                    <label for="player2" class="label">Player 2</label>
                                    <div class="control">
                                        <input type="text" v-model="player2" id="player2" placeholder="Player 2"
                                               class="input" @keyup="updateValues"/>
                                    </div>
                                </div>
                            </div>
                            <div class="column">
                                <div class="field">
                                    <label for="score2" class="label">Score 2</label>
                                    <div class="control">
                                        <input type="number" v-model="score2" id="score2" placeholder="0"
                                               class="input" @keyup="updateValues"/>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </form>
                </div>
                <div class="column">
                    <div class="score-box" v-bind:class="getBackgroundClass()">
                        <div class="tournament">
                            {{ tournament }}
                        </div>
                        <div class="scores">
                            <div class="player">
                                {{ player1 }}
                            </div>
                            <div class="score">
                                {{ score1 }} - {{ score2 }}
                            </div>
                            <div class="player">
                                {{ player2 }}
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="view-score" v-else>
            <div class="score-box" v-bind:class="getBackgroundClass()">
                <div class="tournament">
                    {{ tournament }}
                </div>
                <div class="scores">
                    <div class="player">
                        {{ player1 }}
                    </div>
                    <div class="score">
                        {{ score1 }} - {{ score2 }}
                    </div>
                    <div class="player">
                        {{ player2 }}
                    </div>
                </div>
            </div>
        </div>
        <div>
            <div class="field">
                <label for="formview" class="checkbox">
                    <input type="checkbox" class="checkbox" v-model="form" id="formview">
                    Form view
                </label>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
    data() {
        return {
            factions: {
                "monsters": "Monsters",
                "nilfgaard": "Nilfgaard",
                "northern-realms": "Northern Realms",
                "scoia-tael": "Scoia'Tael",
                "skellige": "Skellige",
            },
            background: "",
            tournament: "",
            player1: "",
            score1: "",
            player2: "",
            score2: "",
            form: true
        };
    },
    methods: {
        getBackgroundClass() {
            return 'bg-' + this.background;
        },
        updateValues() {

        }
    }
});
</script>

<style lang="scss" scoped>
.score-box {
    display: inline-block;
    background-size: 100% 100%;
    background-repeat: no-repeat;

    color: white;
    padding: 10px 40px 10px 30px;
    font-family: "Roboto Slab";
    font-size: 24px;
    line-height: 28px;
    text-align: left;

    $factions: monsters, nilfgaard, northern-realms, scoia-tael, skellige;
    @each $faction in $factions {
        &.bg-#{$faction} {
            background-image: url('/img/#{$faction}-ltr.png');
        }
    }
}

.tournament {
    font-size: 16px;
}

.scores {
    font-family: Gwent;
    display: flex;
    justify-content: flex-end;
    align-items: flex-end;
}

.score {
    padding: 0 15px;
}
</style>