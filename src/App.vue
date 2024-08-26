<template>
  <v-app>
    <v-main>
      <v-container>
        <div v-if="text.length > 0">
          <text-editor 
          :data="text"
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
    TextEditor
  },

  data() {
    return {
      text: []
  }
  },
  methods: {
    async fetchTexts() {
      try {
        const response = await axios.get('https://66cbaa844290b1c4f19ad4a3.mockapi.io/api/text/texts').then(res => res = res.data);
        
        this.text = response
      } catch (error) {
        console.log('Error fetching data', error);
      }
    },
    async changeText(payload) {
      console.log(payload);
      try {
        const response = await axios.put(`https://66cbaa844290b1c4f19ad4a3.mockapi.io/api/text/texts/${payload.id}`, {
          text: payload.text, 
          color: payload.color, 
          font: payload.font,
          alignment: payload.alignment,
        });
        
        this.text = response
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