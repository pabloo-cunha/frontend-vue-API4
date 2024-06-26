<script setup>
import axios from 'axios';
import { useTheme } from 'vuetify'
import { hexToRgb } from '@layouts/utils'
import VueApexCharts from 'vue3-apexcharts'
import { onMounted, ref, computed } from 'vue'

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
  subtitle: {
    type: String,
    required: true,
  },
  labels: {
    type: Array,
    required: true,
  },
  mainInformation: {
    type: String,
    required: true,
  },
  mainInformationSubtitle: {
    type: String,
    required: true,
  },
  series: {
    type: Array,
    required: true,
  },
  orders: {
    type: Array,
    required: true,
  },
  chartOptions: {
    // type: String,
    required: true,
  },
})

</script>

<template>
  <VCard>
    <VCardItem class="pb-3">
      <VCardTitle class="mb-1">
        {{ title }}
      </VCardTitle>
      <VCardSubtitle> {{ subtitle }} </VCardSubtitle>

      <template #append>
        <div class="me-n3 mt-n8">
          <MoreBtn :menu-list="moreList" />
        </div>
      </template>
    </VCardItem>

    <VCardText>
      <div class="d-flex align-center justify-space-between mb-3">
        <div class="flex-grow-1">
          <h4 class="text-h4 mb-1">
            {{ mainInformation }}
          </h4>
          <span> {{ mainInformationSubtitle }} </span>
        </div>

        <div>
          <VueApexCharts
            type="donut"
            :height="125"
            width="105"
            :options="props.chartOptions.value"
            :series="props.series"
          />
        </div>
      </div>

      <VList class="card-list mt-7">
        <VListItem
          v-for="order in props.orders"
          :key="order.title"
        >
          <template #prepend>
            <VAvatar
              rounded
              variant="tonal"
              :color="order.avatarColor"
            >
              <VIcon :icon="order.avatarIcon" />
            </VAvatar>
          </template>

          <VListItemTitle class="mb-1">
            {{ order.title }}
          </VListItemTitle>
          <VListItemSubtitle class="text-disabled">
            {{ order.subtitle }}
          </VListItemSubtitle>

          <template #append>
            <span>{{ order.amount }}</span>
          </template>
        </VListItem>
      </VList>
    </VCardText>
  </VCard>
  </template>

<style lang="scss" scoped>
.card-list {
  --v-card-list-gap: 21px;
}
</style>
