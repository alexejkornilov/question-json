<template>
    <div class="content">
    <form @submit="checkForm">
        <div class="form_question">
            <div class="form_question-field">
                <label for="rawData.part">
                    Часть
                </label>
                <input class="part" id="rawData.part" type="text" v-model="rawData.part" />
            </div>
            <div class="form_question-field">

                <label for="rawData.name">
                    Название
                </label>
                <textarea class="part" id="rawData.name" v-model="rawData.name"></textarea>
            </div>
            <div class="form_question-field">
                <label for="rawData.part">
                    Условия выполнения
                </label>
                <textarea class="part" id="rawData.condition" v-model="rawData.condition"></textarea>
            </div>
            <div class="form_question-field">
                <label for="rawData.time">
                    Время выполнения
                </label>
                <input class="part" id="rawData.time" type="text" v-model="rawData.time"/>
            </div>
            <div class="form_question-field">
                <label for="rawData.questionCount">
                    Количество вопросов
                </label>
                <input class="part" id="rawData.questionCount" type="text" v-model="rawData.questionCount"/>
            </div>
            <fieldset v-for="(block, index) in rawData.blocks" :key="index">
                <div class="form_question-field">
                    <label for="block.part">
                        Часть
                    </label>
                    <input class="part" id="block.part" type="text" v-model="block.part"/>
                </div>
                <div class="form_question-field">
                    <label for="block.name">
                        Название
                    </label>
                    <input class="part" id="block.name" type="text" v-model="block.name"/>
                </div>
                <div class="form_question-field">
                    <label for="block.is_multiple">
                        Множественное
                    </label>
                    <input class="part" id="block.is_multiple" type="checkbox" v-model="block.is_multiple"/>
                </div>
                <fieldset v-for="(question, qindex) in block.questions" :key="qindex">
                    <div class="form_question-field">
                        <label for="question.number">
                            Вопрос #
                        </label>
                        <input class="part" id="question.number" type="number" v-model="question.number"/>
                    </div>
                    <div class="form_question-field">
                        <label for="question.question">
                            Вопрос
                        </label>
                        <textarea class="part" id="question.question" v-model="question.question"></textarea>
                    </div>

                    <div v-for="(answer, aindex) in question.answer" :key="aindex">
                        <div class="form_question-field">
                            <label for="answer.number">
                                Ответ #
                            </label>
                            <input class="part" id="answer.number" type="number" v-model="answer.number"/>
                        </div>
                        <div class="form_question-field">
                            <label for="answer.value">
                                Ответ
                            </label>
                            <textarea class="part" id="answer.value" v-model="answer.value"></textarea>
                        </div>
                    </div>
                    <button v-on:click="addAnswer($event, question.answer, index, qindex)">Добавить ответ</button>
                </fieldset>
                <div class="button" v-on:click="addQuestions($event, block.questions, index)">Добавить вопрос</div>
            </fieldset>
            <div class="button" v-on:click="addBlock($event, rawData.blocks)">Добавить блок вопросов</div>

        </div>
        <button type="submit" value="Сохранить">Сохранить</button>
    </form>
    <div class="result">
        <pre>{{rawData}}</pre>
    </div>
    </div>
</template>

<script>
    export default {
        name: "questionsEdit",
        data() {
            return {
                rawData: {}
            }
        },

        mounted() {
            this.getRawData()
        },
        methods: {
            getRawData() {
                this.rawData = JSON.parse(document.getElementById('data').innerText);
                this.rawData = JSON.parse('{"name":"1","condition":"1","time":"1","blocks":[{"part":"1","name":"1"}]}');
                this.rawData = {};
                console.log(this.rawData);
            },
            checkForm(e) {
                e.preventDefault();
                console.log(JSON.stringify(this.rawData));
            },
            addAnswer(e, question, index, qindex) {
                e.preventDefault();
                if (typeof question == 'undefined') {
                    this.$set(this.rawData.blocks[index].questions[qindex], 'answer', [{}]);
                }
                else {
                    this.$set(this.rawData.blocks[index].questions[qindex].answer, this.rawData.blocks[index].questions[qindex].answer.length, {});
                }
            },
            addBlock(e, block) {
                if (typeof block == 'undefined') {
                    this.$set(this.rawData, 'blocks', [{}]);

                } else {
                    this.$set(this.rawData.blocks, this.rawData.blocks.length, {});
                }
                return true;
            },
            addQuestions(e, questions, index) {
                // e.preventDefault();
                if (typeof questions == 'undefined') {
                    this.$set(this.rawData.blocks[index], 'questions', [{}]);
                }
                else {
                    this.$set(this.rawData.blocks[index].questions, this.rawData.blocks[index].questions.length, {});
                }
                return true;
            },
        }
    }
</script>

<style scoped>
    .content {
        display: flex;
    }
    .form_question {
        display: flex;
        flex-flow: column;
    }

    .form_question-field {
        display: flex;
    }

    .form_question-field label {
        width: 200px;
    }

    .button {
        display:inline-block;
        color:#444;
        border:1px solid #CCC;
        background:#DDD;
        box-shadow: 0 0 5px -1px rgba(0,0,0,0.2);
        cursor:pointer;
        vertical-align:middle;
        max-width: fit-content;
        text-align: center;
    }

    .button:active {
        color:red;
        box-shadow: 0 0 5px -1px rgba(0,0,0,0.6);
    }
</style>
