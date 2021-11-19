<template>
  <table class="table table-hover">
    <thead>
    <tr>
      <th
        v-for="col of columns"
        :key="col"
      >{{ col }}</th>
    </tr>
    </thead>
    <tbody>
    <tr
      v-for="(item, i) of rows"
      :key="i"
      class="packages-table__row"
      @click="selectRow(item.name)"
    >
      <td>
        <img
          :src="item.owner.avatar"
          :alt="item.owner.name"
          :title="item.owner.name"
          class="packages-table__avatar"
        >
      </td>
      <td>
        <div class="packages-table__name mx-auto ellipsis">
          {{ item.name }}
        </div>
      </td>
      <td>
        <div class="packages-table__version mx-auto ellipsis">
          {{ item.version }}
        </div>
      </td>
      <td>
        <div
          :title="item.license"
          class="packages-table__version mx-auto ellipsis"
        >
          {{ item.license }}
        </div>
      </td>
      <td
        :title="item.description"
        class="packages-table__description ellipsis"
      >
        {{ item.description }}
      </td>
    </tr>
    </tbody>
  </table>
  <app-pagination
    :model-value="page"
    :pages-total="pagesTotal"
    class="mt-md-2"
    @update:model-value="selectPage"
  />
</template>

<script>
import AppPagination from '@/components/AppPagination';

export default {
  name: 'PackagesTable',
  components: {
    AppPagination,
  },
  props: {
    rows: {
      type: Array,
      required: true,
    },
    total: {
      type: Number,
      required: true,
    },
    page: {
      type: Number,
      default: undefined,
    },
    rowsPerPage: {
      type: Number,
      default: 10,
    }
  },
  data() {
    return {
      columns: [
        'Автор',
        'Название',
        'Версия',
        'Лицензия',
        'Описание',
      ],
    };
  },
  computed: {
    pagesTotal() {
      return Math.ceil(this.total / this.rowsPerPage);
    },
  },
  emits: ['select-page', 'select-row'],
  methods: {
    selectPage(page) {
      this.$emit('select-page', page);
    },
    selectRow(name) {
      this.$emit('select-row', name);
    },
  },
}
</script>

<style lang="scss" scoped>
  .packages-table {
    &__avatar {
      width: 20px;
      height: 20px;
    }

    &__row {
      cursor: pointer;
      &:hover {
        background: darken(white, 2%);
      }
    }

    &__description {
      max-width: 20em;
      font-size: 0.8em;
      text-align: center;
    }

    &__license, &__version {
      width: 100px;
      text-align: center;
    }

    &__name {
      width: 200px;
      text-align: center;
    }
  }

  .ellipsis {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
  }
</style>
