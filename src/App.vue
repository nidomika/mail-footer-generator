<script setup lang="ts">
import { computed, reactive } from 'vue'
const data = reactive({
  name: 'Imię',
  nick: 'Nick',
  lastName: 'Nazwisko',
  position: 'Stanowisko ds. Stanowiska',
  tel: '123456789',
  email: 'shrek@bagno.com',
})

const displayName = computed(() => {
  if (data.nick) {
    return `${data.name} "${data.nick}" ${data.lastName}`
  }
  return `${data.name} ${data.lastName}`
})
const formattedPhone = computed(() => {
  let phone = data.tel
  if (!phone.startsWith('+48')) {
    phone = `+48${phone}`
  }

  return phone.replace(/\s/g, '').replace(/-/g, '')
})

// copy to clipboard with styles from div of id="mail-footer"
const copyToClipboard = () => {
  const mailFooter = document.getElementById('mail-footer')
  if (mailFooter) {
    const range = document.createRange()
    range.selectNode(mailFooter)
    window.getSelection()?.removeAllRanges()
    window.getSelection()?.addRange(range)
    document.execCommand('copy')
    window.getSelection()?.removeAllRanges()
  }
}
</script>

<template>
  <label class="label">
    <span>Imię </span>
    <input v-model="data.name" />
  </label>
  <label class="label">
    <span>Nazwisko </span>
    <input v-model="data.lastName" />
  </label>
  <label class="label">
    <span>Nick </span>
    <input v-model="data.nick" />
  </label>
  <label class="label">
    <span>Stanowisko </span>
    <input v-model="data.position" />
  </label>
  <label class="label">
    <span>Telefon </span>
    <input v-model="data.tel" type="tel" />
  </label>
  <label class="label">
    <span>Email </span>
    <input v-model="data.email" type="email" />
  </label>
  <button @click="copyToClipboard">Kopiuj</button>

  <hr />

  <div id="mail-footer" style="font-family: sans-serif; font-size: small">
    <p>Pozdrawiam</p>
    <span style="font-weight: 700">{{ displayName }}</span
    ><br />
    <span style="font-style: italic">{{ data.position }}</span
    ><br />
    tel:
    <a :href="`tel:${formattedPhone}`">{{ data.tel }}</a
    ><br />
    email: <a :href="`mailto:${data.email}`">{{ data.email }}</a
    ><br />
    <br />
    <img
      src="https://github.com/nidomika/mail-footer-generator/assets/34137726/f530254a-845a-4660-8ea7-60cdbd53e3bb"
      width="220"
      height="100"
      style="background-color: white"
      alt=""
    /><br />
    Cech Fantastyki "SkierCon"<br />
    <a href="https://skiercon.pl">https://skiercon.pl/</a><br />
    <div id="social" style="padding-top: 10px">
      <a
        href="https://www.facebook.com/SkierCon/"
        style="
          display: inline-block;
          background-color: grey;
          border-radius: 50%;
          width: 32px;
          height: 32px;
          margin-right: 5px;
        "
      >
        <img
          src="https://ssl.gstatic.com/atari/images/sociallinks/facebook_white_28dp.png"
          height="32"
          width="32"
          alt="facebook"
        />
      </a>
      <a
        href="https://www.instagram.com/skiercon/"
        style="
          display: inline-block;
          background-color: grey;
          border-radius: 50%;
          width: 32px;
          height: 32px;
          margin-right: 5px;
        "
      >
        <img
          src="https://ssl.gstatic.com/atari/images/sociallinks/instagram_white_28dp.png"
          height="32"
          width="32"
          alt="instagram"
        />
      </a>
      <a
        href="https://www.youtube.com/@cfskiercon7731"
        style="
          display: inline-block;
          background-color: grey;
          border-radius: 50%;
          width: 32px;
          height: 32px;
          margin-right: 5px;
        "
      >
        <img
          src="https://ssl.gstatic.com/atari/images/sociallinks/youtube_white_28dp.png"
          height="32"
          width="32"
          alt="youtube"
        />
      </a>
      <a
        href="https://www.tiktok.com/@skiercon"
        style="
          display: inline-block;
          background-color: grey;
          border-radius: 50%;
          width: 32px;
          height: 32px;
        "
      >
        <img
          src="https://ssl.gstatic.com/atari/images/sociallinks/tiktok_white_28dp.png"
          height="32"
          width="32"
          alt="tiktok"
        />
      </a>
    </div>
  </div>
</template>

<style>
.label {
  display: block;
  margin-bottom: 10px;
}
body {
  font-family: sans-serif;
  padding: 0;
  font-size: medium;
}
</style>
