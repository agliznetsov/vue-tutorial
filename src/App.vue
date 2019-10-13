<template>
    <div id="app" class="small-container">
        <asset-form :assetId="assetId" @select-asset="selectAsset" @take-snapshot="takeSnapshot()"/>

        <snapshots-view v-if="assetId" :snapshots="snapshots" @select-snapshot="selectSnapshot"/>

        <snapshot-view :snapshot="snapshot"/>
    </div>
</template>

<script>

  import AssetForm from './components/AssetForm.vue'
  import SnapshotsView from "./components/SnapshotsView";
  import SnapshotView from "./components/SnapshotView";

  export default {
    name: "app",
    components: {
      SnapshotsView,
      AssetForm,
      SnapshotView
    },
    data() {
      return {
        assetId: '000',
        snapshots: [],
        snapshot: undefined
      }
    },

    mounted() {
      this.getEmployees()
    },

    methods: {
      async getEmployees() {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users');
          const data = await response.json();
          this.snapshots = data;
        } catch (error) {
          console.error(error);
        }
      },

      selectAsset(assetId) {
        console.log('Selected asset', this.assetId);
        this.assetId = assetId;
      },

      takeSnapshot() {
        console.log('take-snapshot', this.assetId);
      },

      async selectSnapshot(snapshotId) {
        try {
          const response = await fetch('https://jsonplaceholder.typicode.com/users/' + snapshotId);
          this.snapshot = await response.json();
          console.info(this.snapshot.name);
        } catch (error) {
          console.error(error);
        }
      },

      // async addEmployee(employee) {
      //     try {
      //         const response = await fetch('https://jsonplaceholder.typicode.com/users', {
      //             method: 'POST',
      //             body: JSON.stringify(employee),
      //             headers: {"Content-type": "application/json; charset=UTF-8"}
      //         })
      //         const data = await response.json()
      //         // this.employees = [...this.employees, data]
      //     } catch (error) {
      //         console.error(error)
      //     }
      // },
    },
  }
</script>

<style>
    html *
    {
        font-size: 12px;
    }

    .small-container {
        margin: auto;
        max-width: 1200px;
    }

    .VueTables__limit {
        display: none !important;
    }

    .VueTables__table tr {
        cursor: pointer;
    }

</style>
