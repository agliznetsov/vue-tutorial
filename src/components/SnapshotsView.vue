<template>
    <div id="snapshots-view">
        <p v-if="snapshots.length < 1" class="empty-table">
            No snapshots
        </p>
        <v-client-table :columns="columns" :data="snapshots" :options="options" @row-click="onClick" >
            <!--            <a slot="uri" slot-scope="props" target="_blank" :href="props.row.uri" class="glyphicon glyphicon-eye-open">{{props.row.uri}}</a>-->
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
        columns: ['name', 'username', 'email'],
        options: {
          headings: {
            name: 'Name',
            code: 'Username',
            uri: 'Email',
          },
          perPage: 5,
          perPageValues: [5, 10, 50],
          filterable: false
        }
      }
    },
    mounted() {
    },
    methods: {
      onClick(e) {
        console.info("click", e.row.id);
        this.$emit('select-snapshot', e.row.id)
      }
    }
  }
</script>

<style scoped>
    .empty-table {
        text-align: center;
    }
</style>
