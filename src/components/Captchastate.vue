<template>
<component :is="selectedCaptcha" />

</template>

<script>
import Standartcaptcha from '@/components/Standartcaptcha.vue'
import Dotcaptcha from '@/components/Dotcaptcha.vue'
import Questioncaptcha from '@/components/Questioncaptcha.vue';
import Tilecaptcha from '@/components/Tilecaptcha.vue';
import Tilecaptchavar from '@/components/Tilecaptchavar.vue';
import Tilecaptchavar2 from '@/components/Tilecaptchavar2.vue';
import Standartcaptchavar from '@/components/Standartcaptchavar.vue'
import Standartcaptchavar2 from '@/components/Standartcaptchavar2.vue'

export default {
  name: 'Captchastate',
  components: {
    Standartcaptcha,
    Dotcaptcha,
    Tilecaptcha,
    Questioncaptcha,
    Tilecaptchavar,
    Tilecaptchavar2,
    Standartcaptchavar,
    Standartcaptchavar2
  },
  data() {
    return {
      inputValue: '',
      captchas: ["Standartcaptchavar2","Standartcaptchavar",'Standartcaptcha','Standartcaptcha','Standartcaptcha', 'Tilecaptcha', 'Dotcaptcha', 'Questioncaptcha',"Tilecaptchavar2","Tilecaptchavar"]
    };
  },
  computed: {
    selectedCaptcha() {
      const randomIndex = Math.floor(Math.random() * this.captchas.length);
      return this.captchas[randomIndex];
    }
  },
  methods: {
    redirectToError() {
      // Redirect to /error route
      this.$router.push('/error');
    }
  }
};
</script>

