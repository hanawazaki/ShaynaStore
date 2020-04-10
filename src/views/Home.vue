<template>
  <div class="home">
   <HeaderShayna />
   <HeroShayna />
   <WomanBanner />
   <InstaShayna />
   <PartnerLogo />
   <FooterShayna />
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderShayna from '@/components/HeaderShayna.vue'
import HeroShayna from '@/components/HeroShayna.vue'
import WomanBanner from '@/components/WomanBanner.vue'
import InstaShayna from '@/components/InstaShayna.vue'
import PartnerLogo from '@/components/PartnerLogo.vue'
import FooterShayna from '@/components/FooterShayna.vue'

export default {
  name: 'Home',
  components: {
    HeaderShayna,
    HeroShayna,
    WomanBanner,
    InstaShayna,
    PartnerLogo,
    FooterShayna
  }
}
</script>
