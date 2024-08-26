<template>
    <v-container>
        <v-textarea
            v-model="text"
            label="Введите текст"
            @keydown.enter.prevent="handleEnter" 
        />
        <v-select v-model="font" :items="fontOptions" label="Выбор шрифта" />
        <v-select v-model="color" :items="colorOptions" label="Выбор цвета" />
        <v-select v-model="alignment" :items="alignmentOptions" label="Выбор выравнивания" />
        <v-btn @click="$emit('change', payload)">Сохранить</v-btn>

        <v-container class="text-container">
            <div :style="editorStyle" v-html="formattedText"></div>
        </v-container>
    </v-container>
</template>

<script>
import { ref, computed } from 'vue'

export default {
    props: {
        data: {
            type: Array,
            required: true
        }
    },
    setup(props) {
        const text = ref(props.data[0].text)
        const font = ref(props.data[0].font)
        const color = ref(props.data[0].color)
        const alignment = ref(props.data[0].alignment)

        const fontOptions = ['Arial', 'Courier New', 'Georgia', 'Times New Roman']
        const colorOptions = ['black', 'red', 'blue', 'green']
        const alignmentOptions = ['left', 'center', 'right']

        const editorStyle = computed(() => ({
            fontFamily: font.value,
            color: color.value,
            textAlign: alignment.value
        }))

        const formattedText = computed(() => {
            return text.value.replace(/\n/g, '<br>')
        })

        const handleEnter = (event) => {
            const cursorPosition = event.target.selectionStart;
            text.value = text.value.slice(0, cursorPosition) + '\n' + text.value.slice(cursorPosition)
            event.target.setSelectionRange(cursorPosition + 1, cursorPosition + 1)
        }

        const payload = ref({
            id: props.data[0].id,
            text: text,
            font: font,
            color: color,
            alignment: alignment
        })

        return { text, font, color, alignment, fontOptions, colorOptions, alignmentOptions, editorStyle, handleEnter, formattedText, payload }
    }
}
</script>

<style>
    .text-container {
        margin-top: 40px;
        background: #f0f0f0;
        min-height: 56px;
    }
</style>
