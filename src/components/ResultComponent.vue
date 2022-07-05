<template>
  <v-container>
    <v-data-table v-if="headers" :headers="headers" :items="displayableData" class="elevate-5" :items-per-page="10">
      <template v-slot:body="props">
        <tr v-for="(item, i) in props.items" :key="i">
          <td v-for="(headeritem, idx) in headers" :key="idx">{{ item[headeritem.value] }}</td>
        </tr>
      </template>
    </v-data-table>
    <h3 v-else>No Results to Display</h3>
  </v-container>
</template>
<script lang="ts">
import Vue from 'vue';
import { Component, Prop, Watch } from 'vue-property-decorator';
import employees from '../Data/employee';
import customers from '../Data/customers';
import orders from '../Data/order';

@Component
export default class ResultComponent extends Vue {
  @Prop() query!: string;

  public displayableData = '';

  mounted() {
    if (this.query.toLowerCase().includes('emp')) {
      if (this.query.toLowerCase().includes('where')) {
        this.displayableData = employees.filter((x) => x.employeeID === 2);
      } else this.displayableData = employees;
    } else if (this.query.toLowerCase().includes('customer')) {
      this.displayableData = customers;
    } else if (this.query.toLowerCase().includes('order')) {
      this.displayableData = orders;
    }
  }

  get headers() {
    if (this.displayableData) {
      return Object.keys(this.displayableData[0]).map((x) => ({
        text:
          x
            .replace(/([A-Z])/g, ' $1')
            .charAt(0)
            .toUpperCase() + x.replace(/([A-Z])/g, ' $1').slice(1),
        value: x,
      }));
    }
    return null;
  }
}
</script>
<style>
.v-data-table__wrapper > table {
  border-spacing: 10px !important;
  border-collapse: separate;
}
</style>
