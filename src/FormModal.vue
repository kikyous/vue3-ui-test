<template>
  <el-dialog model-value="true" title="新增作业" width="70%">
    <div class="px-4">
      <el-form label-position="left" label-width="100px">
        <el-form-item label="选择在线测试">
          <el-select v-model="ruleForm.groupSet" class="w-full" placeholder="请选择分组方案">
            <el-option label="1">1</el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="标题">
          <el-input />
        </el-form-item>
        <el-form-item label="作业附件">
          <div
            class="flex w-50 h-16 justify-center items-center gap-1.5 border-rd-1 border-0.25 border-solid border-[#B3B3B3] bg-[#F4F4F4]">
            添加文件</div>
        </el-form-item>
        <el-divider />
        <el-form-item label="作业形式" prop="resource">
          <el-radio-group v-model="ruleForm.type">
            <el-radio label="personal"> 个人作业</el-radio>
            <el-radio label="group"> 分组作业</el-radio>
          </el-radio-group>
        </el-form-item>
        <el-form-item label="评分方式">
          <div class="">
            <table class="blueTable radius-1">
              <thead>
                <tr>
                  <th class="p-3">评分方式</th>
                  <th class="p-3"> <el-checkbox></el-checkbox> 教师评阅</th>
                  <th class="p-3"> <el-checkbox></el-checkbox> 学生互评</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td class="px-3 py-2">成绩占比</td>
                  <td class="px-3 py-2">
                    <div class="flex">
                      <el-input class="w-28!" v-model="ruleForm.count" />
                      <div class="whitespace-nowrap ml-2">%</div>
                    </div>
                  </td>
                  <td class="px-3 py-2">
                    <div class="flex">
                      <el-input class="w-28!" v-model="ruleForm.count" />
                      <div class="whitespace-nowrap ml-2">%</div>
                    </div>
                  </td>
                </tr>
                <tr>
                  <td class="p-3">评分设置</td>
                  <td class="p-3"></td>
                  <td class="p-3">
                    <div class="flex items-center">
                      <el-checkbox class="mr-2!"></el-checkbox> 匿名评分
                    </div>

                    <div class="flex items-center">
                      <el-checkbox class="mr-2!"></el-checkbox> 仅提交作业才可参与
                    </div>
                    <div class="flex items-center">
                      <el-checkbox class="mr-2!"></el-checkbox> 未完成互评扣分
                    </div>
                  </td>
                </tr>
                <tr>
                  <td class="p-3">量规</td>
                  <td class="p-3" colspan="2">
                    <el-select class="w-full" placeholder="请选择">
                      <el-option>1</el-option>
                    </el-select>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </el-form-item>
        <el-form-item label="发放">
          <div class="box flex w-full flex-col p-4 gap-6 self-stretch border-rd-1 border-0.25 border-solid">
            <div class="flex">
              <div class="w-30 flex-shrink-0">发放班级</div>
              <el-select class="w-full" placeholder="请选择" v-model="ruleForm.assignClasses" multiple collapse-tags>
                <el-option v-for="item in classes" :key="item" :label="item" :value="item" />
              </el-select>
            </div>
            <div class="flex">
              <div class="w-30 flex-shrink-0">作业截止时间</div>
              <el-date-picker placeholder="选择日期" v-model="ruleForm.submitCloseTime" type="datetime" />
            </div>
            <div class="font-600">学生互评设置</div>

            <div class="flex">
              <div class="w-30 flex-shrink-0">互评时间</div>
              <el-date-picker placeholder="选择日期" v-model="ruleForm.submitCloseTime" type="datetime" />
              <div class="mx-2">
                至
              </div>
              <el-date-picker placeholder="选择日期" v-model="ruleForm.submitCloseTime" type="datetime" />
            </div>
            <div class="flex">
              <div class="w-30 flex-shrink-0">评阅份数</div>
              <div class="flex">
                <el-input class="w-12" v-model="ruleForm.count" />
                <div class="whitespace-nowrap ml-2">份 / 组</div>
              </div>
            </div>

          </div>
          <a href="" class="decoration-none text-[#20BEC8]">
            添加
          </a>
        </el-form-item>
        <el-divider />
        <el-form-item label="成绩比例">
          <div>
            <el-slider class="w-150!" v-model="ruleForm.percent" show-input :marks="marks" />
            <div class="mt-4 text-[#737373]">(总成绩比例不能超过100%，剩余11.4%)</div>
          </div>
        </el-form-item>
        <el-form-item label="完成指标">
          <div>
            <el-radio-group class="" v-model="ruleForm.hasZb">
              <el-radio label="1" size="large">无</el-radio>
              <el-radio label="2" size="large">有</el-radio>
              <el-select placeholder="请选择" v-model="ruleForm.zb">
                <el-option label="提交作业" value="1">提交作业</el-option>
              </el-select>
            </el-radio-group>
            <div class="ml-17 mt-1 flex w-69.75 pt-1 flex-col justify-center items-start bg-[#E9E9E9] rounded-sm p-3">
              设置「完成指标」后，学生需达到条件才算完成。该活动将自动纳入学习分析的完成度统计，并作为学生学习进度的分母条件
            </div>
          </div>

        </el-form-item>
      </el-form>
    </div>
    <template #footer>
      <span class="dialog-footer flex justify-center">
        <el-button type="primary"> 保存 </el-button>
        <el-button type="info">取消</el-button>
      </span>
    </template>
  </el-dialog>
</template>
<script lang="ts" setup>
import { reactive } from 'vue';

const marks = reactive({
  35.6: '35.6',
  100: '100',
})
const classes = ['公路1班', '公路2班', '公路3班'] as const;

const ruleForm = reactive({
  name: 'Hello',
  count: 5,
  assignClasses: [],
  submitCloseTime: '',
  delivery: false,
  type: 'personal',
  percent: 10,
  hasZb: '1',
  zb: '',
  groupSet: ''
})
</script>

<style>
.box {
  border: 1px solid #DFDFDF
}

table.blueTable {
  border: 1px solid #DFDFDF;
  background-color: #FFFFFF;
  width: 100%;
  text-align: left;
  border-collapse: collapse;
  border-radius: 5px;
}

table.blueTable td,
table.blueTable th {
  border: 1px solid #DFDFDF;
}

table.blueTable thead {
  background: #F7F7F7;
}

table.blueTable thead th {
  font-size: 15px;
  color: #000000;
  font-weight: normal;
}
</style>
