<template>
    <v-container>
        <editor-options 
        v-if="showOptions" 
        :style="{ top: `${optionsPosition.top}px`, left: `${optionsPosition.left}px` }"
        >
            <v-select 
            class="selection-option" 
            v-model="font" 
            :items="fontOptions" 
            label="Выбор шрифта" 
            />
            <div class="selection-option color-block " :style="colorBlockStyle"></div>
            <v-select 
            class="selection-option" 
            v-model="color" 
            :items="colorOptions" 
            label="Выбор цвета" 
            />
            <v-select 
            class="selection-option" 
            v-model="alignment" 
            :items="alignmentOptions" 
            label="Выбор выравнивания" 
            />
        </editor-options>
        
        
            <div class="text-container">
                <div
                    class="text-field"
                    contenteditable="true" 
                    @input="updateText"
                    @click="showOptionsMenu($event)"
                    v-html="formattedText"
                    :style="editorStyle"
                >
                </div>
            </div>
            <v-btn class="save-btn" @click="$emit('change', payload)">Сохранить</v-btn>

        
    </v-container>
</template>

<script>
import { ref, computed } from 'vue';
import EditorOptions from './EditorOptions.vue';

export default {
    props: {
        data: {
            type: Array,
            required: true
        }
    },
    components: {
        EditorOptions
    },
    setup(props) {
        const text = ref(props.data[0].text);
        const font = ref(props.data[0].font);
        const color = ref(props.data[0].color);
        const alignment = ref(props.data[0].alignment);
        const showOptions = ref(false);
        const optionsPosition = ref({ top: 0, left: 0 });

        const fontOptions = ['Arial', 'Courier New', 'Georgia', 'Times New Roman'];
        const colorOptions = ['black', 'red', 'blue', 'green'];
        const alignmentOptions = ['left', 'center', 'right'];

        const editorStyle = computed(() => ({
            fontFamily: font.value,
            color: color.value,
            textAlign: alignment.value,
            minHeight: '56px',
            border: '1px solid #ccc',
            padding: '5px',
            cursor: 'text'
        }));

        const formattedText = computed(() => {
            return text.value.replace(/\n/g, '<br>');
        });

        const updateText = (event) => {
            text.value = event.target.innerText;
        };

        const showOptionsMenu = (event) => {
            showOptions.value = true;
            optionsPosition.value = {
                top: event.clientY - 30,
                left: event.clientX + 10,
            };
        };

        const closeOptionsMenu = () => {
            showOptions.value = false;
        };

        const payload = ref({
            id: props.data[0].id,
            text: text,
            font: font,
            color: color,
            alignment: alignment
        })

        console.log('payload', payload);
        

        const colorBlockStyle = computed(() => ({
            backgroundColor: color.value,
            width: '56px',
            height: '56px',
            border: '2px solid #000',
            margin: '0 5px'
        }));

        return { 
            text, font, color, alignment, fontOptions, colorOptions, 
            alignmentOptions, editorStyle, formattedText, 
            colorBlockStyle, showOptions, optionsPosition, updateText, 
            showOptionsMenu, payload, closeOptionsMenu
        }
    }
}
</script>

<style>
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

    .save-btn {
        margin-top: 30px;
        float: right;
    }

    .color-block {
        width: 56px;
        height: 56px;
        outline: 1px solid #000;
        margin: 0 5px;
        border-radius: 8px;
        flex: 1;
    }

    .options-menu {
        position: absolute;
        background-color: white;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        z-index: 10;
        margin-top: 5px;
        padding: 10px;
        height: 80px;
    }

    .selection-option {
        flex: 2;
    }
</style>
