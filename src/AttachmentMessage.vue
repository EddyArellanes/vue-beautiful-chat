<template>
  <div :id="id" class='sc-message--attachment' :style="messageColors">
    <button class="btn arrow-left" @click="slideLeft(id)"> < </button>    
    
    <div class='card' v-for="(card, index) in data.attachments" :key="index">      
      <img :src="card.image_url" alt="Avatar" style="width:100%;height:100px;">
      <div class="container">
        <h4><b>{{card.title}}</b></h4> 
        <p>{{card.subtitle}}</p> 
        <div v-for="(button, index) in card.buttons" :key="index">
          <button 
            class="card-button info" 
            v-if="button.type == 'postback'"          
            @click="_submitPayload(button.payload)">
            {{ button.title}}
          </button>
          <a :href="button.url" v-else-if="button.type == 'web_url'" target="_blank">
            <button 
              class="card-button info"                         
              @click="_submitPayload(button.payload)">
              {{ button.title}}
            </button>
            </a>
        </div>
        
      </div>
    </div>           
    <button class="btn arrow-right" @click="slideRight(id)"> > </button>
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
    },
    onSubmit: {
      type: Function,
      required: true
    },
  },  
  data: () =>{
    return {
      id: String(Date.parse( new Date()))
    }
  },
  mounted(){

  },
  updated(){
    const element = document.getElementById(`${id}`)
    element.scrollLeft = element.scrollLeft  - 200
  },
  methods: {
    _submitPayload( payload) {
      this.onSubmit({author: 'me', type: 'text', data: { text: payload }})
      
    },
    slideRight(id){            
      const element = document.getElementById(`${id}`)
      //Scroll in Attachmend Div from the position + 20      
      if(element.scrollLeft !== element.scrollWidth) {
        
        element.scrollLeft += 80;
      }
      
    },
    slideLeft(id){
      
      
      const element = document.getElementById(`${id}`)
      //Scroll in Attachmend Div from the position + 20
      
      if(element.scrollLeft !== element.scrollWidth) {
        
        element.scrollLeft -= 80;
      }
    }
  }
}
</script>

<style scoped>
.sc-message--attachment {
  position: relative;
  display: -webkit-inline-box;  
  width: 500px;
  overflow-x: hidden;
  padding: 8px 0;
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
  width: 80%;
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
  margin-bottom: 4px;

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
.arrow-button{
  border-radius: 2px;
  border: 1px solid grey;
  background: white;
}
.arrow-left{
  position: sticky;
  left: 0%;
  top: 50%;  
  margin-left: 8px;
}
.arrow-right{
  position: sticky;
  right: 0%;
  top: 50%;
  margin-right: 8px;
}
.btn{
     
    padding: 7px;    
    border-width: 0;
    outline: none;
    border-radius: 2px;
    -webkit-box-shadow: 0 1px 4px rgba(0, 0, 0, .6);
    box-shadow: 0 1px 4px rgba(0, 0, 0, .6);
    background-color: #44a3cf;
    color: #ecf0f1;
    -webkit-transition: background-color .3s;
    transition: background-color .3s;
}
.btn:hover, .btn:focus {
  background-color: #2b6885;
}
.btn:before{
  content: "";
  
  position: absolute;
  top: 50%;
  left: 50%;
  
  display: block;
  width: 0;
  padding-top: 0;
    
  border-radius: 100%;
  
  background-color: rgba(236, 240, 241, .3);
  
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
.btn:active:before {
  width: 120%;
  padding-top: 120%;  
  transition: width .2s ease-out, padding-top .2s ease-out;
}
.btn:before {
  content: "";
  
  position: absolute;
  top: 50%;
  left: 50%;
  
  display: block;
  width: 0;
  padding-top: 0;
    
  border-radius: 100%;
  
  background-color: rgba(236, 240, 241, .3);
  
  -webkit-transform: translate(-50%, -50%);
  -moz-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  -o-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
</style>
