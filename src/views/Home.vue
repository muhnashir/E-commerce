<template>
  <div class="home">
    <HeaderCandleshine />
    <HeroCandleshine />
    <BannerCandleshine />
    <InstaCandleshine />
    <PartnerCandleshine />
    <FooterCandleshine />
    
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderCandleshine from '@/components/HeaderCandleshine.vue'
import HeroCandleshine from '@/components/HeroCandleshine.vue'
import BannerCandleshine from '@/components/BannerCandleshine.vue'
import InstaCandleshine from '@/components/InstaCandleshine.vue'
import PartnerCandleshine from '../components/PartnerCandleshine.vue'
import FooterCandleshine from '../components/FooterCandleshine.vue'


export default {
  name: 'Home',
  components: {
    HeaderCandleshine,
    HeroCandleshine,
    BannerCandleshine,
    InstaCandleshine,
    PartnerCandleshine,
    FooterCandleshine,
  }
}
</script>
