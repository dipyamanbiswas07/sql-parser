<template>
  <v-container>
    <v-row>
      <v-col><h3>Please type in your query or select one from the predefined list</h3></v-col>
    </v-row>
    <v-row>
      <v-col cols="9">
        <v-text-field v-model="sqlQuery" label="Query" clearable hint="Please enter a valid SQL Query" :disabled="showData" @click="onClickClearQuery()"> </v-text-field>
      </v-col>
      <v-col cols="3" class="mt-6">
        <v-row>
          <v-btn class="mr-2" pt-2 :disabled="!isSQLqueryEmpty" @click="onViewResultsClick()"> View Results</v-btn>
          <v-btn pt-2 :disabled="!isSQLqueryEmpty" @click="onClickClearQuery()"> Clear Results</v-btn>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="2">
        <v-select label="Predefined Queries" :items="predefinedQueries" v-model="sqlQuery" :disabled="showData"></v-select>
      </v-col>
    </v-row>
    <result-component v-if="showData" :query="sqlQuery"></result-component>
  </v-container>
</template>
<script lang="ts">
import Vue from 'vue';
import { Component, Prop } from 'vue-property-decorator';
import ResultComponent from './ResultComponent.vue';
import sqlQueryList from './configs';

@Component({
  components: {
    ResultComponent,
  },
})
export default class ParserContainer extends Vue {
  public sqlQuery = '';

  public showData = false;

  get isSQLqueryEmpty() {
    return this.sqlQuery;
  }

  get predefinedQueries() {
    return sqlQueryList;
  }

  onViewResultsClick() {
    this.showData = true;
  }

  onClickClearQuery() {
    this.showData = false;
    this.sqlQuery = '';
  }
}
</script>
