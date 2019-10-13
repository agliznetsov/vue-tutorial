<template>
    <div id="asset-form">
        <div class="input-group mb-3">
            <div class="input-group-prepend">
                <span class="input-group-text">Asset ID</span>
            </div>
            <input type="text" class="form-control" aria-label="asset id" v-model="model.assetId">
            <div class="input-group-append">
                <button @click="selectAsset">Select</button>
                <button @click="takeSnapshot">Take Snapshot</button>
            </div>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'asset-form',
    props: {
      assetId: String
    },
    data() {
      return {
        model: {
          assetId: ''
        }
      }
    },
    methods: {
      selectAsset() {
        this.$emit('select-asset', this.model.assetId);
      },
      takeSnapshot() {
        this.$emit('take-snapshot');
      }
    },
    mounted() {
      let vm = this;

      vm.$nextTick(function () {
        console.log('mounted', vm.assetId);
        vm.model.assetId = vm.assetId;
      });
    }
  }
</script>

