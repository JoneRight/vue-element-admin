<template>
  <div class="app-container">
    <switch-roles @change="handleRolesChange" />
    <el-button @click="choose">click</el-button>
    <el-dialog
      title="提示"
      :visible.sync="dialogVisible"
      width="30%"
      :before-close="handleClose"
    >
      <el-cascader
        ref="tree"
        v-model="selectedIds"
        :options="options"
        :props="props"
        clearable
      />
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import SwitchRoles from './components/SwitchRoles'

export default {
  name: 'PagePermission',
  components: { SwitchRoles },
  data() {
    return {
      dialogVisible: false,
      props: { multiple: true },
      selectedIds: [],
      options: [{
        value: 1,
        label: '东南',
        children: [{
          value: 2,
          label: '上海',
          children: [
            { value: 3, label: '普陀' },
            { value: 4, label: '黄埔' },
            { value: 5, label: '徐汇' }
          ]
        }, {
          value: 7,
          label: '江苏',
          children: [
            { value: 8, label: '南京' },
            { value: 9, label: '苏州' },
            { value: 10, label: '无锡' }
          ]
        }, {
          value: 12,
          label: '浙江',
          children: [
            { value: 13, label: '杭州' },
            { value: 14, label: '宁波' },
            { value: 15, label: '嘉兴' }
          ]
        }]
      }, {
        value: 17,
        label: '西北',
        disabled: true,
        children: []
      }]
    }
  },
  methods: {
    handleRolesChange() {
      this.$router.push({ path: '/permission/index?' + +new Date() })
    },
    choose() {
      this.dialogVisible = true
      console.log(2222)
    },
    handleClose(done) {
      this.$refs.tree.$refs.panel.clearCheckedNodes()
      this.$refs.tree.$refs.panel.activePath = []
      console.log(this.selectedIds)
      done()
    }
  }
}
</script>
