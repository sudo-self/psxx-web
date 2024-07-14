<template>
  <div class="hero min-h-screen bg-base-200">
    <div class="hero-content text-center">
      <div class="max-w-xl">
        <div class="avatar mb-4 mx-auto" data-aos="zoom-in">
          <div class="mask mask-squircle w-24 mx-auto"></div>
        </div>
        <div class="flex justify-center items-center h-80" data-aos="fade-up">
          <img
            :class="{ rotate: showIframe }"
            src="https://pub-c1de1cb456e74d6bbbee111ba9e6c757.r2.dev/final.png"
            alt="Icon"
            class="max-w-full max-h-full rounded-full"
          />
        </div>
        <h1 data-aos="fade-down" class="text-4xl md:text-7xl font-bold mb-6">PSX Web</h1>
        <p data-aos="fade-down" data-aos-delay="300" class="md:text-lg mb-6">
          PSX Web runs&nbsp;<span class="text-green-900">100%&nbsp;</span>in browser. Serving up nostalgia with original Playstation classics direct from the console. Batteries included.
        </p>
        <div class="flex justify-center space-x-5" data-aos="fade-down" data-aos-delay="600">
          <button
            class="btn btn-sm md:btn-md btn-primary"
            @click="playGame"
          >
            Play Now
          </button>
          <select
            v-model="selectedGame"
            @change="loadGame"
            class="select select-bordered w-full max-w-xs"
          >
            <option value="" disabled selected>Playstation Games</option>
            <option value="https://tonyhawk2.vercel.app/">Tony Hawk 2</option>
            <option value="https://metalgearsolid.vercel.app/">Metal Gear Solid</option>
            <option value="https://dracularesurection.vercel.app/">Dracuala Resurection</option>
            <option value="https://coolboarders4.vercel.app/">Cool Boarders 4</option>
            <option value="https://tombraider2.vercel.app/">Tomb Raider 2</option>
            <option value="https://diehard3.vercel.app/">Die Hard 3</option>
            <option value="https://batmanforever.vercel.app/">Batman Forever</option>
            <option value="https://toystory2.vercel.app/">Toy Story 2</option>
            <option value="https://needforspeed3.vercel.app/">Need For Speed 3</option>
            <option value="https://madden2005.vercel.app/">John Madden 05</option>
            <option value="https://finalfantasy9.vercel.app/">Final Fantasy iX</option>
            <option value="https://vigilante8.vercel.app">Vigilante 8</option>
            <option value="https://crashbandicoot.vercel.app/">Crash Bandicoot 2</option>
            <option value="https://streetfighter2.vercel.app/">Street Fighter Alpha</option>
            <option value="https://retro-assembly-puce.vercel.app/">Retro Games</option>
          </select>
          <a
            data-aos="fade-down"
            data-aos-delay="600"
            class="btn btn-sm md:btn-md btn-primary btn-outline"
            href="https://github.com/sudo-self/Playstation"
            target="_blank"
          >
            Star on GitHub
          </a>
        </div>
        <div class="flex justify-center mt-4" data-aos="fade-up" data-aos-delay="900">
          <input
            type="text"
            placeholder="https://"
            class="input input-bordered input-primary w-full max-w-xs"
            v-model="tvUrl"
          />
          <button
            class="btn btn-sm md:btn-md btn-primary ml-2"
            @click="openTv"
          >
            View
          </button>
        </div>
      </div>
    </div>
  </div>
  <generic-panel>
    <div v-if="showIframe" data-aos="flip-down" class="flex flex-col items-center">
      <div class="flex justify-center space-x-2 mb-5">
        <kbd class="kbd">v</kbd>
        <kbd class="kbd">S</kbd>
        <kbd class="kbd">X</kbd>
        <kbd class="kbd">ENTER</kbd>
      </div>
      <div class="outer-tv-frame">
        <div class="inner-tv-frame">
          <iframe
            v-if="showIframe && iframeSrc"
            :src="iframeSrc"
            class="tv-screen"
            allowfullscreen
            ref="gameIframe"
          ></iframe>
          <img
            v-else
            src="https://static.vecteezy.com/system/resources/previews/004/349/996/non_2x/television-screen-error-tv-test-pattern-and-tv-no-signal-concept-smpte-color-bars-illustration-free-vector.jpg"
            alt="Placeholder"
            class="tv-screen"
          />
        </div>
      </div>
      <div data-aos="flip-up">
        <div class="remote-container mt-2 cursor-pointer" @click="closeIframe">
          <img
            src="https://api.iconify.design/game-icons:tv-remote.svg?color=%23919191"
            alt="Close TV"
            class="tv-remote-icon"
          />
          <div class="red-dot bg-red-500 w-1 h-1 rounded-full ml-1"></div>
        </div>
      </div>
    </div>
  </generic-panel>
  <footer class="footer footer-center p-10 bg-base-50">
    <div>
      <section id="about" class="py-12 text-center items-center justify-center">
        <h2 class="text-3xl font-bold"><a href="https://chat.jessejesse.com"><i class="las la-comments"></i> Chat</a></h2>
        <p>Question?</p>
      </section>
      <p class="md:font-bold">
        psxweb.vercel.app&nbsp;100% online.
      </p>
      <p>Copyright © {{ new Date().getFullYear() }} &#10085;&nbsp;JesseJesse.com</p>
    </div>
    <div>
      <div class="grid grid-flow-col gap-4">
        <a href="https://x.com/ilostmyipad" target="_blank">
          <i class="lab la-twitter text-4xl"></i>
        </a>
        <a href="https://github.com/sudo-self/Playstation" target="_blank">
          <i class="lab la-github text-4xl"></i>
        </a>
      </div>
    </div>
  </footer>
</template>

<script>
import { useHead } from '#app';
import { definePageMeta } from '#imports';
import GenericPanel from '~/components/commons/GenericPanel';
import ogBanner from '../assets/images/nuxtwind-daisy-og-banner.jpg';

export default {
  components: {
    GenericPanel,
  },
  data() {
    return {
      showIframe: false,
      selectedGame: null,
      iframeSrc: '',
      tvUrl: '',
    };
  },
  setup() {
    definePageMeta({
      layout: 'default',
    });

    useHead({
      title: 'PSXweb',
      description: 'PSX Web is a collection of original PlayStation games serving up nostalgia. Included is a web viewer. Built with Nuxt.js 3 + Tailwind CSS + Daisy UI.',
      link: [
        { rel: 'icon', type: 'image/png', href: '/favicon.png' },
      ],
      meta: [
        {
          hid: 'og:image',
          name: 'og:image',
          property: 'og:image',
          content: ogBanner,
        },
      ],
    });
  },
  methods: {
    playGame() {
      this.showIframe = true;
    },
    loadGame() {
      this.iframeSrc = this.selectedGame;
      this.showIframe = true;
    },
    openTv() {
      if (this.tvUrl) {
        this.iframeSrc = this.tvUrl;
        this.showIframe = true;
      }
    },
    closeIframe() {
      this.showIframe = false;
      this.iframeSrc = '';
    },
  },
};
</script>

<style>
@keyframes rotate360 {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

.rotate {
  animation: rotate360 10s linear infinite;
}

.outer-tv-frame {
  position: relative;
  width: 100%;
  max-width: 1250px;
  margin: auto;
  padding-top: 56.25%;
  max-height: 900px;
  background: #222;
  border: 16px solid #020617;
  border-radius: 16px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.7);
}

.inner-tv-frame {
  position: absolute;
  top: 2%;
  left: 2%;
  width: 96%;
  height: 96%;
  background: black;
  border: 16px solid #4b5563;
  border-radius: 12px;
  box-shadow: inset 0 0 30px rgba(0, 0, 0, 0.7);
}

.tv-screen {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.7);
  object-fit: contain;
}

.tv-remote-icon {
  width: 64px;
  height: 64px;
  transition: transform 0.3s;
}

.remote-container:hover .tv-remote-icon {
  transform: scale(2.1);
}

.red-dot {
  margin-left: 20px;
}

.footer {
  text-align: center;
}

.footer .footer-center p {
  margin: 0;
}
</style>
