<template>
  <thead>
    <th class="selection__header" v-if="shouldRenderSelection" key="--th-multi">
        <multi-select :selection="selection" :rows="data" />
      </th>
      <th v-for="(col, idx) in columns"
        :key="col.title || col.field || idx"
        :class="col.thClass" :style="col.thStyle">
        <!-- <th> component (thComp) -->
        <component
          v-if="col.thComp"
          :is="forDynCompIs(col.thComp)"
          :column="col"
          :field="col.field"
          :title="col.title"
          v-bind="$props">
          <head-sort v-if="col.sortable && col.thComp" :field="col.field" :query="query" />  
        </component>
        <template v-else>
          {{ col.title }}
        </template>

        <i v-if="col.explain" class="fa fa-info-circle" style="cursor: help" :title="col.explain"></i>
        <head-sort v-if="col.sortable && !col.thComp" :field="col.field" :query="query" />
      </th>
  </thead>
</template>
<script>
import HeadSort from './HeadSort.vue'
import MultiSelect from './MultiSelect.vue'
import props from '../_mixins/props'
import shouldRenderSelection from '../_mixins/shouldRenderSelection'

export default {
  name: 'TableHeader',
  components: { HeadSort, MultiSelect },
  mixins: [props, shouldRenderSelection]
}
</script>
