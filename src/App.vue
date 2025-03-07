<script setup lang="ts">
import { computed, reactive, ref } from 'vue'

const data = reactive({
  name: 'Imię',
  nick: '',
  lastName: 'Nazwisko',
  position: 'Stanowisko ds. Stanowiska',
  email: 'shrek@bagno.com',
})

const displayName = computed(() => {
  if (data.nick) {
    return `${data.name} "${data.nick}" ${data.lastName}`
  }
  return `${data.name} ${data.lastName}`
})

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

const copied = () => {
  const button = document.getElementById('copy-button')
  if (button) {
    button.textContent = 'Skopiowano'
    setTimeout(() => {
      button.textContent = 'Kopiuj'
    }, 2000)
  }
}

const isCech = ref(false)
const websiteURL = computed(() =>
  isCech.value ? 'https://cech.skiercon.pl/' : 'https://skiercon.pl'
)
</script>

<template>
  <div class="wrapper">
    <div class="main">
      <h2>
        Generator stopek mailowych {{ isCech ? 'cechowych' : 'konwentowych' }}
      </h2>
      <button class="button-secondary pure-button" @click="isCech = !isCech">
        {{
          isCech
            ? 'Zmień na konwentowy generator'
            : 'Zmień na cechowy generator'
        }}
      </button>
      <form class="pure-form pure-form-stacked">
        <fieldset>
          <div class="pure-control-group">
            <label for="stacked-name" class="label">Imię</label>
            <input
              v-model="data.name"
              class="stacked-name"
              placeholder="Imię"
            />
          </div>
          <div class="pure-control-group">
            <label for="stacked-lastName" class="label">Nazwisko</label>
            <input
              v-model="data.lastName"
              class="stacked-lastName"
              placeholder="Nazwisko"
            />
          </div>
          <div class="pure-control-group">
            <label for="stacked-nick" class="label">Ksywa</label>
            <input
              v-model="data.nick"
              class="stacked-nick"
              placeholder="Ksywa"
            />
          </div>
          <div class="pure-control-group">
            <label for="stacked-position" class="label">Stanowisko</label>
            <input
              v-model="data.position"
              class="stacked-position"
              placeholder="Stanowisko"
            />
          </div>
          <div class="pure-control-group">
            <label for="stacked-email" class="label">Email</label>
            <input
              v-model="data.email"
              class="stacked-email"
              placeholder="Email"
            />
          </div>
        </fieldset>
      </form>
      <button
        @click="copyToClipboard(), copied()"
        id="copy-button"
        class="pure-button pure-button-primary button-large button-success"
      >
        Kopiuj
      </button>
      <hr />
    </div>
    <div class="preview">
      <div
        id="mail-footer"
        style="font-family: sans-serif; font-size: small; max-width: 50em"
      >
        <span style="font-weight: 700">{{ displayName }}</span
        ><br />
        <span style="font-style: italic">{{ data.position }}</span
        ><br /><br />
        email: <a :href="`mailto:${data.email}`">{{ data.email }}</a
        ><br />
        <a :href="websiteURL"> {{ websiteURL }}</a
        ><br />
        <a :href="websiteURL">
          <img
            :src="
              isCech
                ? 'https://github.com/user-attachments/assets/96bbf802-b14a-405c-9aa5-e66f7822d10e'
                : 'https://github.com/user-attachments/assets/e5e7a304-4133-4b42-8485-1df991e2e521'
            "
            width="220"
            style="background-color: white"
            alt=""
          />
        </a>
        <div id="social" style="padding-top: 10px">
          <a
            :href="
              isCech
                ? 'https://www.facebook.com/cech.fantastyki.skiercon'
                : 'https://www.facebook.com/SkierCon/'
            "
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
    </div>
  </div>
</template>

<style>
.wrapper {
  width: 50em;
  @media screen and (max-width: 50em) {
    width: 100%;
  }
}

body {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0 1em;
  @media screen and (max-width: 50em) {
    display: block;
  }
}

.pure-control-group {
  margin: 0.5em 0;
}

input {
  width: 100%;
}

hr {
  margin: 1em 0;
}

.button-large {
  font-size: 110%;
}

.button-success {
  color: white;
  border-radius: 4px;
  text-shadow: 0 1px 1px rgba(0, 0, 0, 0.2);
  background: rgb(8, 171, 46);
  width: 100%;
}

.button-secondary {
  color: white;
  border-radius: 4px;
  background: rgb(66, 184, 221);
}
</style>
