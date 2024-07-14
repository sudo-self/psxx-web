<template>
  <div :data-theme="theme">
    <div class="navbar fixed bg-base-100 z-40 shadow-sm">
      <div class="navbar-start">
        <div class="dropdown dropdown-hover">
          <div tabindex="0" class="btn btn-ghost md:text-xl">
            <i class="las la-gamepad"></i>Mario
          </div>
          <ul tabindex="0" class="p-2 shadow menu dropdown-content bg-base-100 rounded-box w-52">
            <li>
              <a href="https://marioworld.jessejesse.com" class="menu-title text-blue-600">Mario World</a>
            </li>
            <li>
              <a href="https://tyson.jessejesse.com" class="menu-title text-red-600">PunchOUT</a>
            </li>
            <li>
              <a href="https://punchout.jessejesse.com" class="menu-title text-green-600">Super PunchOUT</a>
            </li>
            <li>
              <a href="https://marioallstars.vercel.app" class="menu-title text-blue-600">Mario All-Stars</a>
            </li>
            <li>
              <a href="https://mariokart64.pages.dev/" class="menu-title text-red-600">Mario Kart 64</a>
            </li>
            <li>
              <a href="https://html-mario.pages.dev/" class="menu-title text-green-600">Markdown Mario</a>
            </li>
            <li>
              <a href="https://mariogolf.vercel.app/" class="menu-title text-blue-600">Mario Golf 64</a>
            </li>
            <li>
              <a href="https://smashbros-gamma.vercel.app/" class="menu-title text-red-600">Smash Bros 64</a>
            </li>
          </ul>
        </div>
      </div>
      <div class="navbar-center hidden lg:flex">
        <ul class="menu menu-horizontal px-1"></ul>
      </div>
      <div class="navbar-end flex items-center">
        <select v-model="theme" class="select select-primary md:w-full md:max-w-xs">
          <option disabled selected>Select Theme</option>
          <option v-for="theme in themes" :value="theme" :key="theme">
            {{ theme }}
          </option>
        </select>
        <div tabindex="0" role="button" class="btn btn-ghost btn-circle avatar ml-2">
          <div class="w-10 rounded-full">
           <a href="https://psxweb.vercel.app/">
            <img
              alt="Tailwind CSS Navbar component"
              src="https://pub-c1de1cb456e74d6bbbee111ba9e6c757.r2.dev/final.png" /></a>
          </div>
        </div>
      </div>
    </div>
    <slot />
    <div class="marquee bg-base-100 py-4">
          <ul class="marquee-content flex space-x-4">
            <li><a href="https://vuejs.org" target="_blank"><i class="lab la-vuejs text-green-500"></i>&nbsp;vue js</a></li>
            <li><a href="https://www.npmjs.com"><i class="lab la-npm text-red-500"></i>&nbsp;npm</a></li>
            <li><a href="https://nodejs.org/en"><i class="lab la-node text-green-500"></i>&nbsp;node js</a></li>
            <li><a href="https://emulatorjs.org"><i class="las la-gamepad text-blue-500"></i>&nbsp;emu js</a></li>
            <li><a href="https://cloudflare.com"><i class="las la-cloud text-orange-500"></i>&nbsp;cloudflare DNS</a></li>
            <li><a href="https://nuxt.com"><i class="las la-mountain text-emerald-800"></i>&nbsp;nuxt 3</a></li>
            <li><a href="https://daisyui.com"><i class="las la-spa text-purple-500"></i>&nbsp;Daisy Ui</a></li>
            <li><a href="https://tailwindcss.com"><i class="lab la-css3-alt text-blue-500"></i>&nbsp;Tailwind</a></li>
            <li><a href="https://apple.com"><i class="lab la-apple text-gray-500"></i>&nbsp;macOS</a></li>
            <li><a href="https://reactnative.dev"><i class="lab la-react text-blue-500"></i>&nbsp;React</a></li>
            <li><a href="https://playstation.com"><i class="las la-gamepad text-red-500"></i>&nbsp;PSX</a></li>
            <li><a href="https://vercel.com"><i class="las la-globe-africa text-white"></i>&nbsp;VERCEL</a></li>
            <li><a href="https://creativecommons.org"><i class="lab la-creative-commons text-gray-500"></i>&nbsp;creative commons</a></li>
          </ul>
        </div>
      </div>

</template>
<script>
import { ref, watch, onMounted } from 'vue';
const THEMES = [
  'light', 'dark', 'cupcake', 'bumblebee', 'emerald', 'corporate', 'synthwave',
  'retro', 'cyberpunk', 'valentine', 'halloween', 'garden', 'forest', 'aqua',
  'lofi', 'pastel', 'fantasy', 'wireframe', 'black', 'luxury', 'dracula',
  'cmyk', 'autumn', 'business', 'acid', 'lemonade', 'night', 'coffee', 'winter'
];
export default {
  setup() {
    const theme = ref(null);
    watch(theme, (value) => {
      localStorage.setItem('daisyui-theme', value);
    });
    onMounted(() => {
      theme.value = localStorage.getItem('daisyui-theme') || 'dark';
    });
    return {
      theme,
      themes: THEMES,
    };
  },
};
</script>

<style>
.marquee {
  overflow: hidden;
  position: relative;
}

.marquee-content {
  display: flex;
  width: max-content;
  animation: marquee 40s linear infinite;
}

.marquee-content > li {
  white-space: nowrap;
}

@keyframes marquee {
  from {
    transform: translateX(100%);
  }
  to {
    transform: translateX(-100%);
  }
}
</style>
