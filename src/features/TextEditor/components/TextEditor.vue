<template>
    <v-container class="text-editor">
        <bubble-menu
        :editor="editor"
        :tippy-options="{ duration: 100 }"
        v-if="editor">
            <div class="bubble-menu">
                <div class="marks">
                    <button @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 384 512">
                            <path d="M0 64C0 46.3 14.3 32 32 32l48 0 16 0 128 0c70.7 0 128 57.3 128 128c0 31.3-11.3 60.1-30 82.3c37.1 22.4 62 63.1 62 109.7c0 70.7-57.3 128-128 128L96 480l-16 0-48 0c-17.7 0-32-14.3-32-32s14.3-32 32-32l16 0 0-160L48 96 32 96C14.3 96 0 81.7 0 64zM224 224c35.3 0 64-28.7 64-64s-28.7-64-64-64L112 96l0 128 112 0zM112 288l0 128 144 0c35.3 0 64-28.7 64-64s-28.7-64-64-64l-32 0-112 0z"/>
                        </svg>
                        </button>
                    <button @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 384 512">
                            <path d="M128 64c0-17.7 14.3-32 32-32l192 0c17.7 0 32 14.3 32 32s-14.3 32-32 32l-58.7 0L160 416l64 0c17.7 0 32 14.3 32 32s-14.3 32-32 32L32 480c-17.7 0-32-14.3-32-32s14.3-32 32-32l58.7 0L224 96l-64 0c-17.7 0-32-14.3-32-32z"/>
                        </svg>
                    </button>
                    <button @click="editor.chain().focus().toggleStrike().run()" :class="{ 'is-active': editor.isActive('strike') }">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
                            <path d="M161.3 144c3.2-17.2 14-30.1 33.7-38.6c21.1-9 51.8-12.3 88.6-6.5c11.9 1.9 48.8 9.1 60.1 12c17.1 4.5 34.6-5.6 39.2-22.7s-5.6-34.6-22.7-39.2c-14.3-3.8-53.6-11.4-66.6-13.4c-44.7-7-88.3-4.2-123.7 10.9c-36.5 15.6-64.4 44.8-71.8 87.3c-.1 .6-.2 1.1-.2 1.7c-2.8 23.9 .5 45.6 10.1 64.6c4.5 9 10.2 16.9 16.7 23.9L32 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l448 0c17.7 0 32-14.3 32-32s-14.3-32-32-32l-209.9 0-.4-.1-1.1-.3c-36-10.8-65.2-19.6-85.2-33.1c-9.3-6.3-15-12.6-18.2-19.1c-3.1-6.1-5.2-14.6-3.8-27.4zM348.9 337.2c2.7 6.5 4.4 15.8 1.9 30.1c-3 17.6-13.8 30.8-33.9 39.4c-21.1 9-51.7 12.3-88.5 6.5c-18-2.9-49.1-13.5-74.4-22.1c-5.6-1.9-11-3.7-15.9-5.4c-16.8-5.6-34.9 3.5-40.5 20.3s3.5 34.9 20.3 40.5c3.6 1.2 7.9 2.7 12.7 4.3c0 0 0 0 0 0s0 0 0 0c24.9 8.5 63.6 21.7 87.6 25.6c0 0 0 0 0 0l.2 0c44.7 7 88.3 4.2 123.7-10.9c36.5-15.6 64.4-44.8 71.8-87.3c3.6-21 2.7-40.4-3.1-58.1l-75.7 0c7 5.6 11.4 11.2 13.9 17.2z"/>
                        </svg>
                    </button>
                </div>
                <div class="vertical-line"></div>
                <div class="fonts">
                    <button @click="editor.chain().focus().setFontFamily('Inter').run()" :class="{ 'is-active': editor.isActive('textStyle', { fontFamily: 'Inter' }) }">
                    Inter
                    </button>
                    <button @click="editor.chain().focus().setFontFamily('Comic Sans MS, Comic Sans').run()" :class="{ 'is-active': editor.isActive('textStyle', { fontFamily: 'Comic Sans MS, Comic Sans' }) }">
                    Comic Sans
                    </button>
                    <button @click="editor.chain().focus().setFontFamily('serif').run()" :class="{ 'is-active': editor.isActive('textStyle', { fontFamily: 'serif' }) }">
                    Serif
                    </button>
                    <button @click="editor.chain().focus().setFontFamily('monospace').run()" :class="{ 'is-active': editor.isActive('textStyle', { fontFamily: 'monospace' }) }">
                    Monospace
                    </button>
                    <button @click="editor.chain().focus().setFontFamily('cursive').run()" :class="{ 'is-active': editor.isActive('textStyle', { fontFamily: 'cursive' }) }">
                    Cursive
                    </button>
                    <button @click="editor.chain().focus().unsetFontFamily().run()">
                    Default
                    </button>
                </div>
                <div class="vertical-line"></div>
                <div class="alignment">
                    <button @click="editor.chain().focus().setTextAlign('left').run()" :class="{ 'is-active': editor.isActive({ textAlign: 'left' }) }">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
                            <path d="M288 64c0 17.7-14.3 32-32 32L32 96C14.3 96 0 81.7 0 64S14.3 32 32 32l224 0c17.7 0 32 14.3 32 32zm0 256c0 17.7-14.3 32-32 32L32 352c-17.7 0-32-14.3-32-32s14.3-32 32-32l224 0c17.7 0 32 14.3 32 32zM0 192c0-17.7 14.3-32 32-32l384 0c17.7 0 32 14.3 32 32s-14.3 32-32 32L32 224c-17.7 0-32-14.3-32-32zM448 448c0 17.7-14.3 32-32 32L32 480c-17.7 0-32-14.3-32-32s14.3-32 32-32l384 0c17.7 0 32 14.3 32 32z"/>
                        </svg>
                    </button>
                    <button @click="editor.chain().focus().setTextAlign('center').run()" :class="{ 'is-active': editor.isActive({ textAlign: 'center' }) }">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
                            <path d="M352 64c0-17.7-14.3-32-32-32L128 32c-17.7 0-32 14.3-32 32s14.3 32 32 32l192 0c17.7 0 32-14.3 32-32zm96 128c0-17.7-14.3-32-32-32L32 160c-17.7 0-32 14.3-32 32s14.3 32 32 32l384 0c17.7 0 32-14.3 32-32zM0 448c0 17.7 14.3 32 32 32l384 0c17.7 0 32-14.3 32-32s-14.3-32-32-32L32 416c-17.7 0-32 14.3-32 32zM352 320c0-17.7-14.3-32-32-32l-192 0c-17.7 0-32 14.3-32 32s14.3 32 32 32l192 0c17.7 0 32-14.3 32-32z"/>
                        </svg>
                    </button>
                    <button @click="editor.chain().focus().setTextAlign('right').run()" :class="{ 'is-active': editor.isActive({ textAlign: 'right' }) }">
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512">
                            <path d="M448 64c0 17.7-14.3 32-32 32L192 96c-17.7 0-32-14.3-32-32s14.3-32 32-32l224 0c17.7 0 32 14.3 32 32zm0 256c0 17.7-14.3 32-32 32l-224 0c-17.7 0-32-14.3-32-32s14.3-32 32-32l224 0c17.7 0 32 14.3 32 32zM0 192c0-17.7 14.3-32 32-32l384 0c17.7 0 32 14.3 32 32s-14.3 32-32 32L32 224c-17.7 0-32-14.3-32-32zM448 448c0 17.7-14.3 32-32 32L32 480c-17.7 0-32-14.3-32-32s14.3-32 32-32l384 0c17.7 0 32 14.3 32 32z"/>
                        </svg>
                    </button>
                </div>
                <div class="vertical-line"></div>
                <div class="color">
                    <input
                    class="input-color"
                    type="color"
                    @input="editor.chain().focus().setColor($event.target.value).run()"
                    :value="editor.getAttributes('textStyle').color"
                    >
                </div>
            </div>
        </bubble-menu>

        <floating-menu :editor="editor" :tippy-options="{ duration: 100 }" v-if="editor">
            <div class="floating-menu">
                <button @click="editor.chain().focus().toggleHeading({ level: 1 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }">
                H1
                </button>
                <button @click="editor.chain().focus().toggleHeading({ level: 2 }).run()" :class="{ 'is-active': editor.isActive('heading', { level: 2 }) }">
                H2
                </button>
                <button @click="editor.chain().focus().toggleBulletList().run()" :class="{ 'is-active': editor.isActive('bulletList') }">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
                        <path d="M40 48C26.7 48 16 58.7 16 72l0 48c0 13.3 10.7 24 24 24l48 0c13.3 0 24-10.7 24-24l0-48c0-13.3-10.7-24-24-24L40 48zM192 64c-17.7 0-32 14.3-32 32s14.3 32 32 32l288 0c17.7 0 32-14.3 32-32s-14.3-32-32-32L192 64zm0 160c-17.7 0-32 14.3-32 32s14.3 32 32 32l288 0c17.7 0 32-14.3 32-32s-14.3-32-32-32l-288 0zm0 160c-17.7 0-32 14.3-32 32s14.3 32 32 32l288 0c17.7 0 32-14.3 32-32s-14.3-32-32-32l-288 0zM16 232l0 48c0 13.3 10.7 24 24 24l48 0c13.3 0 24-10.7 24-24l0-48c0-13.3-10.7-24-24-24l-48 0c-13.3 0-24 10.7-24 24zM40 368c-13.3 0-24 10.7-24 24l0 48c0 13.3 10.7 24 24 24l48 0c13.3 0 24-10.7 24-24l0-48c0-13.3-10.7-24-24-24l-48 0z"/>
                    </svg>
                </button>
            </div>
        </floating-menu>

        <editor-content :editor="editor" class="editor-content" />
        <v-btn class="save-btn" @click="$emit('change', payload)">Сохранить</v-btn>
    </v-container>
</template>

<script>
import { ref } from 'vue';

import { useEditor, EditorContent, BubbleMenu, FloatingMenu  } from '@tiptap/vue-3'
import { Color } from '@tiptap/extension-color'
import StarterKit from '@tiptap/starter-kit'
import Heading from '@tiptap/extension-heading'
import Paragraph from '@tiptap/extension-paragraph'
import Text from '@tiptap/extension-text'
import Document from '@tiptap/extension-document'
import FontFamily from '@tiptap/extension-font-family'
import TextStyle from '@tiptap/extension-text-style'
import TextAlign from '@tiptap/extension-text-align'
import Focus from '@tiptap/extension-focus'

export default {
    props: {
        data: {
            type: Array,
            required: true
        }
    },

    components: {
        EditorContent,
        BubbleMenu,
        FloatingMenu
    },
    setup(props) {
        const text = ref(props.data[0].text);
        let editorContent = ref(`
        ${[...text.value].join("")}
        `)

        const editor = useEditor({
        content: editorContent.value,
        extensions: [
            StarterKit,
            Heading.configure({levels: [1, 2, 3]}),
            Paragraph,
            Document,
            Text,
            TextStyle,
            FontFamily,
            Focus.configure({
                className: 'has-focus',
                mode: 'all',
            }),
            Color,
            TextAlign.configure({
                types: ['heading', 'paragraph'],
                defaultAlignment: 'left'
            }),
        ],
        onUpdate: ({ editor }) => {
            updatePayload(editor.getHTML())
        },
        })

        const updatePayload = (newContent) => {
            payload.value.text = newContent;
        }
        
        const payload = ref({
            id: props.data[0].id,
            text: editorContent.value
        })

        return { 
            text,
            payload, 
            editor,
            editorContent
        }
    }
}
</script>

<style>
    .text-editor {
        box-sizing: border-box;
        padding: 40px 0;
        align-items: center;
        display: flex;
        flex-direction: column;
        
    }

    h1, h2, h3, ul {
        margin-top: 10px;
        margin-bottom: 15px;
    }

    ul {
        box-sizing: border-box;
        padding: 0 40px;
    }

    p, li {
        margin: 8px 0;
    }

    .text-container {
        box-sizing: border-box;
        padding: 20px;
        position: relative;
        margin-top: 40px;
        background: #f0f0f0;
        min-height: 56px;
        cursor: text;
        display: flex;
        flex-direction: column;
    }

    .text-field {
        outline: none;
        border: none;
    }

    .ProseMirror-focused {
        border: none;
        outline: none;
    }

    .bubble-menu {
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        display: flex;
        align-items: center;
        justify-items: flex-start;
        box-sizing: border-box;
        padding: 5px 2px;
        background: #fff;
        border: 1px solid #b6b6b6;
        border-radius: 5px;
        min-width: 550px;
        position: relative;
        left: -130px
    }

    .bubble-menu button {
        background-color: unset;
        margin-right: 10px;
        border-radius: 5px;
        transition: all .2s ease;
        box-sizing: border-box;
        padding: 5px;
        font-size: 16px;   
    }

    .bubble-menu button svg {
        width: 20px;
        height: 20px;
    }
    .bubble-menu button:hover {
        background-color: rgb(190, 190, 190);
    }

    .bubble-menu button.is-active {
        background-color: #8e2edb;
        color: #fff;
    }

    .bubble-menu button.is-active:hover {
        background-color: #a73cff;
    }

    .input-color {
        cursor: pointer;
        width: 30px;
        height: 30px;
    }

    .vertical-line {
        width: 1px;
        height: 60px;
        background: #c8c8c8;
        margin: 0 5px;
    }

    .marks {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }

    .marks button,
    .alignment button {
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .fonts {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
    }

    .alignment {
        display: grid;
        grid-template-columns: 1fr 1fr;
    }

    .floating-menu {
        display: flex;
        flex-direction: row;
        position: relative;
        right: 190px;
        box-sizing: border-box;
        padding: 8px;
        border-radius: 8px;
        background: #fefefe;
        border: 1px solid #adadad;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
    }

    .floating-menu button {
        box-sizing: border-box;
        padding: 5px;
        transition: all .2s ease;
        border-radius: 8px;
        font-size: 16px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .floating-menu button svg {
        width: 20px;
        height: 20px;
    }

    .floating-menu button:last-child {
        margin: 0;
    }

    .floating-menu button.is-active {
        background: #8e2edb;
        color: #fff;
    }

    .floating-menu button.is-active:hover {
        background: #8e2edb;
        color: #fff;
    }

    .floating-menu button:hover {
        background: #e0e0e0;
    }

    .has-focus {
    border-radius: 3px;
    box-shadow: 0 0 0 2px #dcdcdc
    }

    .editor-content {
        box-shadow: 0 0px 20px rgba(0, 0, 0, 0.2);
        width: 1400px;
        padding: 40px 60px;
        box-sizing: border-box;
        border-radius: 15px;
        border: 2px solid #e5e5e5;
    }

    .save-btn {
        align-self: center;
        position: fixed;
        left: 40px;
    }

</style>
