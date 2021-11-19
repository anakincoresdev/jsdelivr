<template>
  <div class="wrapper">
    <div class="container-fluid py-xl-5 px-md-5">
      <div class="container">
        <app-field
          v-model="query"
          placeholder="Введите название пакета"
        />
      </div>
    </div>
    <div
      v-if="packages.list.length"
      class="container"
    >
      <div>
        <packages-table
          :rows="packages.list"
          :total="packages.size"
          :page="pagination.page"
          @select-row="selectPackage"
          @select-page="setPage"
        />
      </div>
    </div>
    <package-dialog
        v-model="packageInfoOpened"
        :package-name="selectedPackage"
    />
  </div>
  <app-footer />
</template>

<script>
import AppField from '@/components/AppField';
import PackagesTable from '@/components/packages/PackagesTable';
import PackageDialog from '@/components/packages/PackageDialog';
import AppFooter from "@/components/layouts/AppFooter";
import { SEARCH_PACKAGES } from "@/store/action.types";

export default {
  name: 'App',
  components: {
    AppField,
    AppFooter,
    PackagesTable,
    PackageDialog,
  },
  data() {
    return {
      query: '',
      pagination: {
        page: 1,
        hitsPerPage: 10,
      },
      selectedPackage: null,
      packageInfoOpened: false,
    };
  },
  computed: {
    packages() {
      return this.$store.getters.packages;
    },
  },
  watch: {
    query() {
      this.pagination.page = 1;
      this.search(this.pagination);
    },

    pagination: {
      deep: true,
      handler(value) {
        this.search(value);
      },
    },
  },
  methods: {
    setPage(page) {
      this.pagination.page = page;
    },

    search() {
      const payload = {
        query: this.query,
        ...this.pagination,
      };

      this.$store.dispatch(SEARCH_PACKAGES, payload);
    },

    selectPackage(packageName) {
      this.selectedPackage = packageName;
      this.packageInfoOpened = true;
    },
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #3f3f3f;
}

body {
  height: 100%;
}

.wrapper {
  min-height: calc(100vh - 100px);
}
</style>
