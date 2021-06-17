<template>
  <el-container>
    <el-main>
      <el-row :gutter="20" type="flex" align="top" justify="center">
        <el-col :md="9">
          <TotalBalance :total="totalBalance" />
          <BudgetList :list="list" @deleteItem="onDeleteItem" />
        </el-col>
        <el-col :md="9">
          <Form @submitForm="onFormSubmit" />
        </el-col>
        <el-col :md="9">
          <Dialog />
        </el-col>
      </el-row>
    </el-main>
  </el-container>

</template>

<script>
import BudgetList from "@/components/BudgetList";
import TotalBalance from "@/components/TotalBalance";
import Form from "@/components/Form";
import Dialog from "@/components/Dialog";

export default {
  name: 'App',
  components: {
    BudgetList,
    TotalBalance,
    Form,
    Dialog
  },
  data: () => ({
    list: {
      1: {
        type: 'Income',
        value: 100,
        comment: 'Some comment',
        id: 1
      },
      2: {
        type: 'Outcome',
        value: -50,
        comment: 'Some outcome comment',
        id: 2
      },
      3: {
        type: 'Outcome',
        value: -12,
        comment: 'Twelve',
        id: 3
      },
      4: {
        type: 'Outcome',
        value: -8,
        comment: 'Eight',
        id: 4
      }
    }
  }),
  computed: {
    totalBalance() {
      return Object.values(this.list).reduce(
          (acc, item) => acc + item.value,
          0
      );
    }
  },
  methods: {
    onDeleteItem(id) {
      delete this.list[id];
    },
    onFormSubmit: function (data) {
      const newObj = {
        ...data,
        id: String(Math.random())
      };
      this.list[newObj.id] = newObj;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
}

.green {
  color: #67C23A;
}
.red {
  color: #F56C6C;
}
</style>
