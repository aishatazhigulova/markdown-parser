<template>
    <div class="container">
        <div class="wrapper">
            <h2 class="title">Redactor</h2>
            <textarea ref="textarea"  class="textarea" v-model="markdown"></textarea>
        </div>

        <div class="wrapper">
            <h2 class="title">Preview</h2>
            <div class="text-wrapper">
                <button class="btn" @click="onCopy">
                    <img src="../assets/copy.svg" />
                </button>
                <div class="text" v-html="markdownToHtml"></div>
            </div>
        </div>
    </div>
</template>
<script>
import {marked} from 'marked';
export default {
    name: 'markdown',
    data(){
        return {
            markdown:  "# Type anything",
        };
    },
    computed: {
        markdownToHtml() {
            const text = marked(this.markdown, { sanitize: true })
            return text
        },
    },
    watch: {
        markdown() {
            localStorage.setItem('marked', JSON.stringify(this.markdown))
        }
    },
    methods: {
        onCopy() {
            let textAreaVal = document.querySelector('textarea').value
            navigator.clipboard.writeText(marked(textAreaVal)).then(() => {
                console.log('copied');
            }, (err) => {
                console.log('could not copy', err);
                alert('could not copy', err)
            });
        }
    },
    mounted() {
        this.$refs.textarea.focus()
        if (localStorage.getItem('marked') !== null) {
            this.markdown = JSON.parse(localStorage.getItem('marked'))
        }
    },
}
</script>
<style>
.container {
    margin-top: 100px;
    display: flex;
    gap: 100px;
}

.wrapper {}

.title {
    text-align: center;
    color: yellowgreen;
    margin-bottom: 20px;
}

.textarea {
    border-radius: 8px;
    border: 1px solid transparent;
    background-color: #0e151e;
    color: #FFFFFF;
}

textarea:focus {
    outline: none;
}

.textarea, .text-wrapper {
    width: 500px;
    max-width: 500px;
    min-height: 300px;
    padding: 10px;
}

.text-wrapper {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    position: relative;

}

.btn {
    background: none;
    border: 1px solid transparent;
    position: absolute;
    top: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.btn:active {
    transform: scale(0.9);
}

img {
    cursor: pointer;
    width: 20px;
    height: 20px;
}

.text > * {
    word-wrap: break-word;
    white-space: pre-wrap;
    word-break: break-word;
}


@media only screen and (max-width: 600px) {
    .container {
        flex-direction: column;
        width: 100%;
    }

    .textarea, .text-wrapper {
        width: 100%;
        height: 100%;
    }

    .title {
        margin-bottom: 10px;
    }
}
</style>
