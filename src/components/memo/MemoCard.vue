<script setup lang="ts">
import RadarChart from '@/components/common/RadarChart.vue'

withDefaults(
  defineProps<{
    name?: string
    iconUrl?: string
    createdAt?: Date
    updatedAt?: Date
    summary?: string
    status?: number[]
  }>(),
  {
    name: 'hello',
    iconUrl: '',
    createdAt: () => new Date('0000/01/01'),
    updatedAt: () => new Date('0000/01/01'),
    summary: '',
    status: () => [0, 0, 0, 0, 0],
  }
)
</script>

<template>
  <v-card variant="outlined" class="px-2" style="border: 1px solid lightgray">
    <v-row>
      <v-col>
        <v-row>
          <v-col cols="12" sm="6" md="4" lg="4" xl="4">
            <div :style="$vuetify.display.xs ? 'width:120px;' : 'width: 80%;'">
              <v-img
                :src="iconUrl"
                :class="$vuetify.display.xs ? 'my-1' : 'ma-1'"></v-img>
            </div>
          </v-col>
          <v-col v-if="$vuetify.display.smAndDown">
            作成日:{{ createdAt.toLocaleDateString() }}<br />
            更新日:{{ updatedAt.toLocaleDateString() }}
          </v-col>
        </v-row>
      </v-col>
      <v-col v-if="!$vuetify.display.smAndDown" class="text-caption">
        作成日:{{ createdAt.toLocaleDateString() }}<br />
        更新日:{{ updatedAt.toLocaleDateString() }}
      </v-col>
      <v-col class="d-flex justify-end">
        <v-btn icon flat>
          <v-icon>mdi-pencil-box-outline</v-icon>
        </v-btn>
        <v-btn icon flat>
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-col>
    </v-row>
    <v-row dense>
      <v-col>
        <g-span :text="name" bold />
      </v-col>
    </v-row>
    <v-row dense>
      <v-col>
        <v-divider />
      </v-col>
    </v-row>
    <v-row class="flex-row-reverse">
      <v-col cols="12" sm="6" md="3" lg="3" xl="2">
        <radar-chart
          :labels="['a', 'b', 'c', 'd', 'e']"
          :data-list="[{ name: name || '', values: status }]" />
      </v-col>
      <v-col cols="12" sm="6" md="9" lg="9" xl="10">
        <g-span :text="summary" />
      </v-col>
    </v-row>
  </v-card>
</template>

<style scoped></style>
