
<script>
import { ref } from "vue";
export default {
  name: "Pastebin",
  setup() {
    function base64ToBytes(base64) {
      const binString = atob(base64);
      return new TextDecoder().decode(
        Uint8Array.from(binString, (m) => m.codePointAt(0))
      );
    }
    var decodedPaste = "Error: Invalid paste";
    try{
        const url = new URL(window.location.href);
        const encodedPaste = url.pathname.substring(1);
        const paste = encodedPaste; // Do not decode, decode in client
        decodedPaste = base64ToBytes(paste);
    }catch(e) {
        
    }

    const msg = ref(decodedPaste);
    const showmsg = ref(false);

    return {
      msg,
      showmsg,
    };
  },
  mounted() {
    navigator.clipboard.writeText(self.msg);
    this.showMessage();
  },
  methods: {
    showMessage() {
      this.showmsg = true;
      setTimeout(() => {
        this.showmsg = false;
      }, 3000);
    },
    onclick() {
      navigator.clipboard.writeText(self.msg);
      this.showMessage();
    },
  },
};
</script>
<template>
  <div class="container">
    <div class="textbox">{{ msg }}</div>
    <input type="button" value="COPY" @click="onclick" />
  <div class="msgbox" :class="{ show: showmsg }">
    <span >Copied to clipboard!</span></div>
  </div>
</template>

<style>
textarea {
  resize: none;
}
.msgbox {
  visibility: hidden;
  opacity: 0;
  position: fixed;
  content: "Copied to clipboard!";
  margin: auto;
  left: 0;
  right: 0;
  top: 80vh;
  width: 150px;
  border-style: solid;
  border-radius: 10px;
  border-width: 1px;
  border-color: var(--placeholder);
  text-align: center;
  padding: 10px 2em;
  background-color: var(--white-blue);
  transition: opacity 0.2s ease-in-out, visibility 0.2s;
  color: var(--blue);
  font-size: 12px;
  font-weight: 100;
}

.show {
  visibility: visible;
  opacity: 0.8;
  transition: opacity 0.2s ease-in-out, backdrop-filter 0.2s;

  backdrop-filter: blur(0px);
}
</style>