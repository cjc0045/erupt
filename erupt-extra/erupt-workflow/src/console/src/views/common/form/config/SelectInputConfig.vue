<template>
  <div>
    <el-form-item label="提示文字">
      <el-input v-model="value.placeholder" placeholder="请设置提示语" size="small"/>
    </el-form-item>
    <el-form label-position="top">
      <el-form-item class="options" label="选项设置">
        <div slot="label" class="option-item-label">
          <span>选项设置</span>
          <el-button icon="el-icon-plus" size="mini" type="text"
                     @click="value.options.push('新选项')">新增选项</el-button>
        </div>
        <draggable :list="value.options" :options="dragOption" group="option" handler=".el-icon-rank">
          <div v-for="(op, index) in value.options" :key="index" class="option-item">
            <i class="el-icon-rank"></i>
            <el-input v-model="value.options[index]" clearable placeholder="请设置选项值" size="medium">
              <el-button slot="append" icon="el-icon-delete" size="medium" type="danger"
                         @click="value.options.splice(index, 1)"></el-button>
            </el-input>
          </div>
        </draggable>

      </el-form-item>
    </el-form>
    <el-form-item label="选项展开">
      <el-switch v-model="value.expanding"></el-switch>
    </el-form-item>

  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "SelectInputConfig",
  components: {draggable},
  props:{
    value:{
      type: Object,
      default: ()=>{
        return {}
      }
    }
  },
  data() {
    return {
      dragOption:{
        animation: 300,
        sort: true
      }
    }
  },
  methods: {}
}
</script>

<style lang="less" scoped>
/deep/ .options{
  .el-form-item__label{
    display: block;
    width: 100%;
    text-align: left;
  }
  .el-icon-rank{
    padding-right: 5px;
    cursor: move;
  }
  .option-item{
    .el-input{
      width: 250px;
      float:right;
    }
  }
}

.option-item-label{
  height: 30px;
  line-height: 30px;
  button{
    float:right;
  }
}

/*/deep/ .el-form-item {
  margin-bottom: 10px;

  .el-form-item__label {
    padding: 0;
  }
  .options{
    .el-icon-rank{
      cursor: move;
    }
  }
}*/
</style>
