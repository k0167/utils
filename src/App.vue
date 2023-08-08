<script setup>
</script>

<template>
  <div>
    <div class="btn-area">
      <button @click="copy">Copy</button>
      <button @click="paste">Paste</button>
      <button @click="format">Format</button>
     
      <button @click="colors" >Colors</button>
      <button @click="fontUp"  >+A</button>
      <button @click="fontDown">
        -<small>
          A
        </small>
      </button>
    </div>
    <textarea spellcheck="false" class="texta" v-model="code" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      code: "",
    };
  },
  methods: {
    copy() {
      navigator.clipboard.writeText(this.code);
    },
    paste() {
      var userAgent = navigator.userAgent.toLowerCase();
      if(userAgent.match(/firefox|fxios/i)){
        alert("Firefox doesn't support clipboard reading");
        return;
      }
      navigator.clipboard.readText().then((text) => {
        this.code = text;
      });
    },
    format() {
      var json = JSON.parse(this.code);
      this.code = JSON.stringify(json, null, 3);
    },
    colors(){
        alert("Not Working today, will be fixed soon");
        return;
  
    },
    fontUp() {
      const style = window.getComputedStyle(document.querySelector(".texta"));
      const fontSize = parseFloat(style.fontSize);
      document.querySelector(".texta").style.fontSize = fontSize + 1 + "px";
    },
    fontDown() {
      const style = window.getComputedStyle(document.querySelector(".texta"));
      const fontSize = parseFloat(style.fontSize);
      document.querySelector(".texta").style.fontSize = fontSize - 1 + "px";
    },
  },  
};
</script>

<style scoped>
textarea {
  height: 500px;
  width: 1000px;
  background-color: #060606;
  color: #fff;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 10px;
  font-size: 14px;
  line-height: 1;
  resize: none;
  /* disable resizing */
}

.btn-area {
  display: flex;
  width: 300px;
  justify-content: space-between;
  margin-bottom: 10px;
}
</style>
