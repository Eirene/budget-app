<template>
  <div class="budget-list-wrap">
    <el-card class="box-card" :header="header">
      <template v-if="!isEmpty">
        <el-alert type="warning" :title="title"></el-alert>
      </template>
      <template>
        <div class="card-header">
          <span>{{ header }}</span>
        </div>
      </template>

      <div class="filter">
        <el-radio-group v-model="radio">
          <el-radio :label="'All'">All</el-radio>
          <el-radio :label="'Income'">Only Income</el-radio>
          <el-radio :label="'Outcome'">Only Outcome</el-radio>
        </el-radio-group>
      </div>

      <template v-for="(item, prop) in list" :key="prop">
        <BudgetListItem
            :typeSelected="typeSelected"
            :type="item.type"
            :comment="item.comment"
            :value="item.value"
            :id="item.id"
            @deleteItem="this.$emit('deleteItem', $event)"
        />
      </template>
    </el-card>
  </div>
</template>

<script>
import BudgetListItem from "@/components/BudgetListItem";

export default {
  name: 'BudgetList',
  components: {
    BudgetListItem,
  },
  props: {
    list: {
      type: Object,
      default: () => ({

      })
    }
  },
  data: () => ({
    header: 'Budget List',
    title: 'Empty list',
    radio: 'All'
  }),
  computed: {
    isEmpty() {
      return Object.keys(this.list).length;
    },
    typeSelected() {
      return this.radio;
    }
  },
  methods: {
  }
}
</script>

<style>
.filter{
  border-bottom: 1px solid #EBEEF5;
  padding: 0 20px 20px;
  margin: 0 -20px 20px;
}
</style>
