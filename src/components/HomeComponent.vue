<template>
  <div class="hello">
    <div>
      <div class="btns">
        <button v-show="showUndo" @click="undoText" class="btn">Undo</button>
      <button v-show="showRedo" @click="redoText" class="btn">Redo</button>
      </div>
      <div>
        <textarea
          v-model="text"
          @input="showUndo = true"
        class="doc-area"
        id="doc-area"
        ></textarea>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeComponent",
  props: {
    msg: String,
  },
  data() {
    return {
      text: "",
      lastAlphabet: [],
      showUndo: false,
      showRedo: false,
    };
  },
  methods: {
    undoText() {
      const newTextArray = this.text.split("");
      this.showRedo = newTextArray.length > 0;
      this.showUndo = this.lastAlphabet.length > 0;
      if (newTextArray.length > 0) {
        this.lastAlphabet.push(newTextArray.pop());
        this.text = newTextArray.join("");
      }
    },
    redoText() {
      const newTextArray = this.text.split("");
      this.showUndo = newTextArray.length > 0;
      this.showRedo = this.lastAlphabet.length > 0;
      if (this.lastAlphabet.length > 0) {
        newTextArray.push(this.lastAlphabet.pop());
        this.text = newTextArray.join("");
      }
    }
  },
  watch: {
    text:function(){
      this.showUndo=this.text.length>0
    }    
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn{
  background:#0f8575 ;
  padding: 10px 30px;
  margin: auto 10px;
  border: none;
  border-radius: 20px;
}
#doc-area{
  min-height: calc(95vh - 7rem); /* subtract the height
  of navbar and footer */
  width: 100%;
}
.btns{
  position: fixed;
  top: 0%;
  left: 0%;
  display: inline-block;
  width: 100%;
}
</style>
