
<script>
import { ref } from "vue";
export default {
    name: 'Pastebin',
    setup() {
        const url = new URL(window.location.href);
        const encodedPaste = url.pathname.substring(1);
        const paste = encodedPaste; // Do not decode, decode in client
        const decodedPaste = decodeURIComponent(encodeURI(atob(paste)));

        navigator.clipboard.writeText(self.msg);
        const msg = ref(decodedPaste);
        const showmsg = ref(false);
        return {
            msg,
            showmsg
        }
    }, 
    methods:{
        
        onclick() {
            navigator.clipboard.writeText(self.msg);
            this.showmsg = true;
            setTimeout(() => {
                this.showmsg = false;
            }, 3000);
        }

    }
}
</script>
<template>
    <div class="container">
        <textarea class="textbox" :value="msg" readonly></textarea>
        <input type="button" value="COPY" @click="onclick">
        <span class="msgbox" :class='{show: showmsg}'>Copied to clipboard!</span> 
    </div>
</template>

<style>
textarea {
    resize: none;
}
.msgbox {
    visibility: hidden;
    opacity: 0;
    position: absolute;
    content: 'Copied to clipboard!';
    margin: auto 30%;
    left: 0;
    right: 0;
    top: 80%;
    border-style: none;
    border-radius: 10px;
    text-align: center;
    padding: 10px;
    background-color: var(--blue);
    transition: opacity 0.2s ease-in-out, visibility 0.2s ;
}
.show {
    visibility: visible;
    opacity: 1;
    transition: opacity 0.2s ease-in-out;
}

</style>