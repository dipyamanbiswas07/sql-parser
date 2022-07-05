<template>
  <div>
    <v-simple-table v-if="headers">
      <template v-slot:default>
        <thead>
          <tr>
            <th v-for="(item, i) in headers" :key="i" class="text-left">{{ item }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, i) in displayableData" :key="i">
            <td v-for="(headeritem, idx) in headers" :key="idx">{{ item[headeritem] }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
    <h3 v-else>No Results to Display</h3>
  </div>
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
      this.displayableData = employees;
    } else if (this.query.toLowerCase().includes('customer')) {
      this.displayableData = customers;
    } else if (this.query.toLowerCase().includes('order')) {
      this.displayableData = orders;
    }
  }

  get headers() {
    if (this.displayableData) return Object.keys(this.displayableData[0]);
    return null;
  }
}
</script>
