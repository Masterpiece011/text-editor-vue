<template>
  <v-app>
    <v-main>
      <v-container class="main__text-editor">
        <h1>Текстовый редактор</h1>
        <div v-if="texts.length > 0">
          <text-editor 
          :data="texts"
          @change="changeText"
          />
        </div>
        <div v-else>Идет загрузка...</div>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import TextEditor from '@/features/TextEditor/components/TextEditor.vue'

import axios from 'axios';

export default {
  name: 'App',

  components: {
    TextEditor,
  },

  data() {
    return {
      texts: []
  }
  },
  methods: {
    async fetchTexts() {
      try {
        const response = await axios.get('https://66cbaa844290b1c4f19ad4a3.mockapi.io/api/text/texts').then(res => res = res.data);
        
        this.texts = response
        console.log(response);
        
      } catch (error) {
        console.log('Error fetching data', error);
      }
    },
    async changeText(payload) {
      console.log('PAYLOAD', payload);
      try {
        const response = await axios.put(`https://66cbaa844290b1c4f19ad4a3.mockapi.io/api/text/texts/${payload.id}`, {
          text: payload.text,
        });
        
        this.texts = response
      } catch (error) {
        console.log('Error changing data', error);
      }
      this.fetchTexts()
    }
  },
  mounted() {
    this.fetchTexts()
  }
}
</script>

<style>
  .main__text-editor {
    box-sizing: border-box;
    padding: 50px;
  }
</style>