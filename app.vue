<template>
    <div>
        <h1>Pintura Image Editor</h1>

        <h2>Inline</h2>

        <div style="height: 70vh">
            <PinturaEditor
                v-bind="editorProps"
                :src="inlineSrc"
                @pintura:load="handleInlineLoad($event)"
                @pintura:process="handleInlineProcess($event)"
            />
        </div>

        <p v-if="inlineResult">
            <img :src="inlineResult" alt="" />
        </p>
    </div>
</template>

<script>
import '@pqina/pintura/pintura.css';

// vue-pintura
import { PinturaEditor } from '@pqina/vue-pintura';

// pintura
import { getEditorDefaults } from '@pqina/pintura';

export default {
    name: 'App',
    components: {
        PinturaEditor,
    },
    methods: {
        // inline
        handleInlineLoad: function (event) {
            console.log('inline load', event.detail);
        },
        handleInlineProcess: function (event) {
            console.log('inline process', event.detail);
            this.inlineResult = URL.createObjectURL(event.detail.dest);
        },
    },
    data() {
        return {
            aspectRatio: undefined,

            // defaults
            editorProps: {
                ...getEditorDefaults(),
            },

            // inline state
            inlineSrc: 'image.jpeg',
            inlineResult: undefined,
        };
    },
};
</script>

<style>
html {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}

h1 {
    margin-top: 0;
}

body {
    padding: 2em;
}

img {
    max-width: 100%;
}

.pintura-editor {
    box-shadow: 0 0 0 1px #eee;
}
</style>
