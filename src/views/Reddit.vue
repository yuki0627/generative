<template>
  <div class="mx-auto max-w-3xl p-2 text-left">
    <p>Images from the on-chain asset provider.</p>
    <ProviderView assetProvider="reddit" />
    <Mint
      :network="network"
      :tokenGated="true"
      :tokenAddress="tokenAddress"
      :tokenGateAddress="tokenGateAddress"
      :restricted="'On-Chain Splatter'"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useRoute } from "vue-router";
import Mint from "@/components/Mint.vue";
import ProviderView from "@/components/ProviderView.vue";
import { addresses } from "@/utils/addresses";

export default defineComponent({
  components: {
    ProviderView,
    Mint,
  },
  setup() {
    const route = useRoute();
    const network =
      typeof route.query.network == "string" ? route.query.network : "goerli";
    const tokenAddress = addresses.redditToken[network];
    const tokenGateAddress = addresses.splatterToken[network];
    console.log("*** chainId", network, tokenAddress);
    return {
      network,
      tokenAddress,
      tokenGateAddress,
    };
  },
});
</script>
