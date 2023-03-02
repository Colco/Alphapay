<script setup lang="ts">
import { ref, reactive } from "vue";
import { ElMessage } from 'element-plus'
import { findTradeSituation } from '~/api/api';
import { useRouter, useRoute } from 'vue-router'
import { useStore } from '~/store/store';

const store = useStore()

const router = useRouter();
const route = useRoute();

interface  DataLog {
  totalTradeAmount: number
  totalPoundage: number
  totalActualIncome: number
  totalPaidOrderNum: number
  totalOrderNum: number
  totalSuccessRate: number

  monthTradeAmount: number
  monthPoundage: number
  monthActualIncome: number
  monthOrderNum: number
  monthPaidOrderNum: number
  monthSuccessRate: number

  todayTradeAmount: number
  todayPoundage: number
  todayActualIncome: number
  todayOrderNum: number
  todayPaidOrderNum: number
  todaySuccessRate: number

  yesterdayTradeAmount: number
  yesterdayPoundage: number
  yesterdayActualIncome: number
  yesterdayOrderNum: number
  yesterdayPaidOrderNum: number
  yesterdaySuccessRate: number
}

let sitlog = reactive(<DataLog>{});
findTradeSituation().then(res => {
    sitlog = res.data.data;
})

</script>

<template>
  <div class="charts-box">
    <div class="card-box">
    <el-card class="box-card">
        <template #header>
        <div class="card-header">
            <span>{{$t('datalog.title1')}}</span>
            <!-- <el-button class="button" type="primary">重置</el-button> -->
        </div>
        </template>
        <div>
            <h1>{{sitlog.totalTradeAmount}}VAD</h1>
        </div>
        <div class="tips">
            <p>{{$t('datalog.service_charge')}}: <span>{{sitlog.todayPoundage}}VAD</span></p>
            <p>{{$t('datalog.paid_in_amount')}}: <span>{{sitlog.todayActualIncome}}VAD</span></p>
        </div>
        <div class="tips">
            <p>{{$t('datalog.order_quantity_paid')}}: <span>{{sitlog.totalPaidOrderNum}}</span></p>
            <p>{{$t('datalog.order_quantity')}}: <span>{{sitlog.todayOrderNum}}</span></p>
            <p>{{$t('datalog.success_rate')}}: <span>{{sitlog.todaySuccessRate}}%</span></p>
        </div>
  </el-card>
  <el-card class="box-card">
        <template #header>
        <div class="card-header">
            <span>{{$t('datalog.title3')}}</span>
            <!-- <el-button class="button" type="primary">重置</el-button> -->
        </div>
        </template>
        <div>
            <h1>{{sitlog.monthTradeAmount}}VAD</h1>
        </div>
        <div class="tips">
            <p>{{$t('datalog.service_charge')}}: <span>{{sitlog.monthPoundage}}VAD</span></p>
            <p>{{$t('datalog.paid_in_amount')}}: <span>{{sitlog.monthActualIncome}}VAD</span></p>
        </div>
        <div class="tips">
            <p>{{$t('datalog.order_quantity_paid')}}: <span>{{sitlog.monthPaidOrderNum}}</span></p>
            <p>{{$t('datalog.order_quantity')}}: <span>{{sitlog.monthOrderNum}}</span></p>
            <p>{{$t('datalog.success_rate')}}: <span>{{sitlog.monthSuccessRate}}%</span></p>
        </div>
  </el-card>
  <el-card class="box-card">
        <template #header>
        <div class="card-header">
            <span>{{$t('datalog.title2')}}</span>
            <!-- <el-button class="button" type="primary">重置</el-button> -->
        </div>
        </template>
        <div>
            <h1>{{sitlog.yesterdayTradeAmount}}VAD</h1>
        </div>
        <div class="tips">
            <p>{{$t('datalog.service_charge')}}: <span>{{sitlog.yesterdayPoundage}}VAD</span></p>
            <p>{{$t('datalog.paid_in_amount')}}: <span>{{sitlog.yesterdayActualIncome}}VAD</span></p>
        </div>
        <div class="tips">
            <p>{{$t('datalog.order_quantity_paid')}}: <span>{{sitlog.yesterdayPaidOrderNum}}</span></p>
            <p>{{$t('datalog.order_quantity')}}: <span>{{sitlog.yesterdayOrderNum}}</span></p>
            <p>{{$t('datalog.success_rate')}}: <span>{{sitlog.yesterdaySuccessRate}}%</span></p>
        </div>
  </el-card>
  <el-card class="box-card">
        <template #header>
        <div class="card-header">
            <span>{{$t('datalog.title4')}}</span>
            <!-- <el-button class="button" type="primary">重置</el-button> -->
        </div>
        </template>
        <div>
            <h1>{{sitlog.todayTradeAmount}}VAD</h1>
        </div>
        <div class="tips">
            <p>{{$t('datalog.service_charge')}}: <span>{{sitlog.todayPoundage}}VAD</span></p>
            <p>{{$t('datalog.paid_in_amount')}}: <span>{{sitlog.todayActualIncome}}VAD</span></p>
        </div>
        <div class="tips">
            <p>{{$t('datalog.order_quantity_paid')}}: <span>{{sitlog.todayPaidOrderNum}}</span></p>
            <p>{{$t('datalog.order_quantity')}}: <span>{{sitlog.todayOrderNum}}</span></p>
            <p>{{$t('datalog.success_rate')}}: <span>{{sitlog.todaySuccessRate}}%</span></p>
        </div>
  </el-card>
    </div>
  </div>
</template>

<style lang="scss" scoped>
$bg:#2d3a4b;
$dark_gray:#889aa4;
$light_gray:#eee;
.card-box {
    padding: 20px;
    display: flex;
    h1 {
        color: #da3764;
    }
    .card-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .tips {
        &:last-child {
            display: block;
        }
        display: flex;
        justify-content: space-between;
        p {
            margin-right: 20px;
            span {
                font-weight: bold;
            }
        }
    }
}
.el-card {
    width: 270px;
    margin-right: 20px;
}
</style>
