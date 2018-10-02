<template>
    <section class="console">
        <div class="header">
            <span class="close" @click="close"></span>
            <span class="minimize" @click="minimize"></span>
            <span class="maximize" @click="maximize"></span>
        </div>
        <div class="container">
        <div class="content">
            <div class="content-inner">
                
            </div>
            <div class="content-input">    
                <span class="content-prefix">rubenbielen.com$</span><input class="content-input-text" @keydown.enter="submit" type="text">
            </div>
        </div>
        </div>
    </section>
</template>

<script>
function consoleExecutor(command) {
    switch (command) {
        default:
            return 'Command not recognized...'
            break;
    }
}

function constructResult(command) {
    const INNER_CLI = `
        <div class="content-inner-cli">
            ${PREFIX}${command}
        </div>
    `;
    const INNER_RESULT = `
        <div class="content-inner-result">
            ${consoleExecutor(command)}
        </div>
    `;
    return INNER_CLI + INNER_RESULT;
}

const PREFIX = '<span class="content-prefix">rubenbielen.com$</span>';

export default {
    methods: {
        close(e) {
            console.log('Not implemented');
        },
        minimize() {
            let section = document.querySelector('section');
            section.classList.remove('fullscreen');
        },
        maximize() {
            let section = document.querySelector('section');
            section.classList.add('fullscreen');
        },
        submit(e) {
            let contentInner = document.querySelector('.content-inner');
            contentInner.innerHTML = contentInner.innerHTML + constructResult(e.target.value);
            e.target.value = '';
            this.setContainer()
        },
        setContainer() {
            let contentInner = document.querySelector('.content');
            let container = document.querySelector('.container');
            let height = contentInner.getBoundingClientRect().height;
            container.style.height = height + 10 + "px";
        }
    },
    mounted() {
        this.setContainer();
    }
}
</script>

<style lang="scss">
@import 'assets/scss/global';

.console {
    border-radius: 5px;
    background-color: $console-background;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    height: 600px;
    width: 800px;
    &.fullscreen {
        height: 100%;
        width: 100%;
    }
    .container {
        position: relative;
        max-height: calc(100% - 28px);
        overflow: hidden;
        bottom: 0;
    }
    .header {
        display: flex;
        flex-direction: row;
        align-items: center;
        border-radius: 5px 5px 0 0;
        font-size: 16px;
        padding-left: 0.2rem;
        line-height: 1.5rem;
        background-color: $console-header;
        color: $console-text-dark;
        font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
        .close {
            display: flex;
            border-radius: 50%;
            width: 12px;
            height: 12px;
            background: $close;
            margin: 0.5rem 0.3rem;
        }
        .minimize {
            display: flex;
            border-radius: 50%;
            width: 12px;
            height: 12px;
            background: $minimize;
            margin: 0.5rem 0.2rem;
        }
        .maximize {
            display: flex;
            border-radius: 50%;
            width: 12px;
            height: 12px;
            background: $maximize;
            margin: 0.5rem 0.3rem;
        }
    }
    .content {
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
        margin: 5px;
        &-input {
            font-family: 'Courier New', Courier, monospace;
            font-size: 14px;
            color: lightgray;
            display: flex;
            &-text {
                font-family: inherit;
                font-size: inherit;
                color: inherit;
                outline: 0;
                border: 0;
                background: transparent;
                caret-color: lightgray;
                width: 100%;
            }
        }
        &-inner {
            color: lightgray;
            font-family: 'Courier New', Courier, monospace;
            font-size: 14px;
            width: 100%;
            &-result {
                margin-bottom: 28px;
            }
        }
        &-prefix {
            color: lightgreen;
            margin-right: 0.5rem;
        }
    }
}
</style>

