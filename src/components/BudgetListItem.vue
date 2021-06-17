<template>
  <div class="budget-item" v-if="typeSelected === 'All' || typeSelected === type">
    <div>
      {{ comment }}
    </div>
    <div class="ml-auto">
      <span class="budget-value" :class="classType">
        {{ value }} <i :class="classIcon"></i>
      </span>
      <el-button type="danger" size="small" @click="$emit('deleteItem', id)">Delete</el-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BudgetListItem',
  props: {
    typeSelected: {
      type: String
    },
    type: {
      type: String
    },
    comment: {
      type: String
    },
    value: {
      type: Number
    },
    id: {
      type: Number
    }
  },
  data: () => ({
  }),
  computed: {
    classIcon() {
      if (this.value > 0){
        return 'el-icon-top';
      }
      return 'el-icon-bottom';
    },
    classType() {
      if (this.value > 0){
        return 'green';
      }
      return 'red';
    },
  },
  methods: {
  }
}
</script>

<style>
.budget-item{
  display: flex;
  align-items: center;
  text-align: left;
  padding: 0.5rem;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
.ml-auto{
  margin-left: auto;
}
</style>
