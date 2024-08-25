<template>
    <v-container>
        <v-textarea v-model="text" label="Введите текст" />
        <v-select v-model="font" :items="fontOptions" label="Выбор шрифта" />
        <v-select v-model="color" :items="colorOptions" label="Выбор цвета" />
        <v-select v-model="alignment" :items="alignmentOptions" label="Выбор выравнивания" />
        <div :style="editorStyle">{{ text }}</div>
    </v-container>
</template>

<script>
import { ref, computed, watch } from 'vue';

export default {
props: {
    data: {
    type: Array,
    required: true
    }
},
setup(props) {
    const text = ref(props.data[0].text);
    const font = ref(props.data[0].font);
    const color = ref(props.data[0].color);
    const alignment = ref(props.data[0].alignment);

    const fontOptions = ['Arial', 'Courier New', 'Georgia', 'Times New Roman'];
    const colorOptions = ['black', 'red', 'blue', 'green'];
    const alignmentOptions = ['left', 'center', 'right'];

    const editorStyle = computed(() => ({
    fontFamily: font.value,
    color: color.value,
    textAlign: alignment.value
    }));

    // watch за изменением props.data
    watch(() => props.data, (newVal) => {
    if (newVal.length > 0) {
        text.value = newVal[0].text;
        font.value = newVal[0].font;
        color.value = newVal[0].color;
        alignment.value = newVal[0].alignment;
    }
    }, { immediate: true });

    return { text, font, color, alignment, fontOptions, colorOptions, alignmentOptions, editorStyle };
}
};
</script>
