<template>
    <div id="snapshots-view">
        <p v-if="snapshots.length < 1" class="empty-table">
            No snapshots
        </p>
        <v-client-table :columns="columns" :data="snapshots" :options="options" @vuetable:row-clicked="onClick" @vuetable:initialized="init">
            <!--            <a slot="uri" slot-scope="props" target="_blank" :href="props.row.uri" class="glyphicon glyphicon-eye-open">{{props.row.uri}}</a>-->
            <!--            <button @click="$emit('select-snapshot', employee.id)">Show</button>-->
        </v-client-table>

    </div>
</template>

<script>
  import Event from 'vue-tables-2'

  export default {
    name: 'snapshots-view',
    props: {
      snapshots: Array,
    },
    data() {
      return {
        columns: ['name', 'code', 'uri'],
        options: {
          headings: {
            name: 'Country Name',
            code: 'Country Code',
            uri: 'View Record',
          },
          perPage: 5,
          perPageValues: [5, 10, 50],
          filterable: false
        }
      }
    },
    mounted() {
      // Event.$on('vue-tables.loaded', function (data) {
      //       console.info("loaded", data);
      // });
    },
    methods: {
      onClick(data) {
        console.info("click", data);
      },
      init(data) {
        console.info("init", data);
      }
    }
  }
</script>

<style scoped>
    .empty-table {
        text-align: center;
    }
</style>
