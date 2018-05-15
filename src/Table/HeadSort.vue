<template>
  <a class="ntv-table-header__sort" href="#" @click.prevent="handleClick" name="HeadSort">
    <i class="ntv-table-header__sort-icon">
      <font-awesome-icon :icon="currArrow" size="xs" />
    </i>
  </a>
</template>
<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import faArrowUp from '@fortawesome/fontawesome-free-solid/faLongArrowAltUp';
import faArrowDown from '@fortawesome/fontawesome-free-solid/faLongArrowAltDown';
import faExchangeAlt from '@fortawesome/fontawesome-free-solid/faExchangeAlt';

/**
 * Sorting arrows within <th>
 */
export default {
  name: 'HeadSort',
  components: {
    FontAwesomeIcon
  },
  props: {
    field: { type: String, required: true },
    query: { type: Object, required: true }
  },
  data: () => ({
    order: ''
  }),
  computed: {
    currArrow() {
      switch (this.order) {
        case 'asc':
          return this.arrowUp;
        case 'desc':
          return this.arrowDown;
        default:
          return this.arrowBoth;
      }
    },
    arrowUp() {
      return faArrowUp;
    },
    arrowDown() {
      return faArrowDown;
    },
    arrowBoth() {
      return faExchangeAlt;
    }
  },
  watch: {
    query: {
      handler({ sort: field, order }) {
        this.order = field === this.field ? order : '';
      },
      deep: true,
      immediate: true
    }
  },
  methods: {
    handleClick() {
      const { query, order } = this;
      query.sort = this.field;
      query.order = this.order = order === 'desc' ? 'asc' : 'desc';
    }
  }
};
</script>
