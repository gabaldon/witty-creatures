<template>
  <div class="prize">
    <img class="prize-icon" :src="url" alt="prize" />
    <h3 class="title">
      {{ title }}
    </h3>
    <a
      class="claimed"
      :class="{ ['eth-highlight']: ethClaimed }"
      :href="'https://etherscan.io/address/' + ethAddress"
      target="_blank"
    >
      {{
        ethClaimed == null
          ? $t('prize.checking')
          : ethClaimed
          ? $t('prize.eth_claimed')
          : $t('prize.eth_unclaimed')
      }}
    </a>
    <a
      class="claimed"
      :class="{ ['wit-highlight']: witClaimed }"
      :href="'https://witnet.network/search/' + witAddress"
      target="_blank"
    >
      {{ $t('prize.check_manually') }}
    </a>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    ethAddress: {
      type: String,
      required: true,
    },
    ethClaimed: {
      type: Boolean,
      required: false,
    },
    witAddress: {
      type: String,
      required: true,
    },
    witClaimed: {
      type: Boolean,
      required: false,
    },
    img: {
      type: String,
      required: true,
    },
  },
  computed: {
    url() {
      return require(`@/assets/svg/${this.img}.svg`)
    },
  },
}
</script>

<style lang="scss" scoped>
.prize {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
  .title {
    font-size: 18px;
    margin-right: 16px;
  }
  .prize-icon {
    margin-right: 16px;
  }
  .claimed {
    padding: 8px;
    border-radius: 4px;
    background-color: grey;
    color: white;
    font-weight: bold;
    margin-right: 16px;
    &:last-of-type {
      margin-right: 0;
    }
  }
  .eth-highlight {
    background-color: #7825ff;
  }
  .wit-highlight {
    background-color: #24cf9c;
  }
}

@media screen and (max-width: 1200px) {
  .prize {
    .title {
      margin-top: 16px;
    }
    .prize-icon {
      margin-top: 16px;
    }
    .claimed {
      margin-top: 16px;
      &:last-of-type {
        margin-right: 0;
      }
    }
  }
}
</style>
