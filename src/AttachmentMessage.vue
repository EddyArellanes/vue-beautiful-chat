<template>
  <div class='sc-message--attachment' :style="messageColors">
    <div class='card' v-for="(card, index) in data.attachments" :key="index">      
      <img :src="card.image_url" alt="Avatar" style="width:100%;height:100px;">
      <div class="container">
        <h4><b>{{card.title}}</b></h4> 
        <p>{{card.subtitle}}</p> 
        <button 
            class="card-button info" 
            v-for=""
            @click="sendMessage(card.buttons.payload)">
            {{card.buttons[0].title}}
        </button>
        
      </div>
    </div>           
  </div>
</template>

<script>
import Suggestions from './Suggestions.vue'
export default {
  components:{
    Suggestions
  },
  props: {
    data: {
      type: Object,
      required: true
    },
    messageColors: {
      type: Object,
      required: true
    }
  },
  mounted(){
    console.log("Attachments")
    console.log(this.data.attachments)
  },
  methods: {
    sendMessage( payload){
      console.log( payload)
    }
  }
}
</script>

<style scoped>
.sc-message--attachment {
  display: -webkit-inline-box;
  overflow-y: hidden;
  padding: 8px 20px;
  border-radius: 6px;
  font-weight: 300;
  font-size: 12px;
  line-height: 1.2;
  /*white-space: pre-wrap;*/
  -webkit-font-smoothing: subpixel-antialiased;    
}

.sc-message--meta {
  font-size: xx-small;
  color: #000;
  margin-bottom: 0px;
  margin-top: 5px;  
  text-align: center;
}
.card {
  display: block;
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 100%;
  margin-bottom: 8px;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}
.card-button{
  border: 1px solid black;
  color: black;
  padding: 3px 12px;
  font-size: 12px;
  cursor: pointer;
  margin-right: 4px;

}
.container {
  padding: 2px 16px;
}
/* Blue */
.info {
  border-color: #2196F3;
  color: dodgerblue;
}
.info:hover {
  background: #2196F3;
  color: white;
}

</style>
