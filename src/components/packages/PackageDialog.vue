<template>
  <app-dialog
    :model-value="modelValue"
    :title="packageName"
    @update:model-value="updateModelValue"
  >
    <template v-if="package">
      <div class="d-flex align-items-center justify-content-between">
        <div class="d-flex align-items-center">
          <img
              :src="package.owner.avatar"
              alt=""
              class="package-dialog__avatar"
          >
          <span class="mx-2">{{ package.owner.name }}</span>
          <span>{{ package.version }}</span>
          <span class="mx-2">{{ package.license }}</span>
        </div>
        <span>Загрузок за последний месяц: {{ package.humanDownloadsLast30Days }}</span>
      </div>
      <p class="text-start my-3">
        {{ package.description }}
      </p>
      <div class="d-flex flex-wrap">
        <div
          v-for="word of package.keywords"
          class="card py-1 px-2 me-2 mb-2"
        >
          {{ word }}
        </div>
      </div>
    </template>
  </app-dialog>
</template>

<script>
import AppDialog from '@/components/AppDialog';
import { GET_PACKAGE_INFO } from "@/store/action.types";

export default {
  name: 'PackageDialog',
  components: {
    AppDialog,
  },
  props: {
    modelValue: {
      type: Boolean,
      default: false,
    },
    packageName: {
      type: String,
      required: true,
    }
  },
  computed: {
    package() {
      return this.$store.getters.package;
    },
  },
  watch: {
    packageName(value) {
      this.$store.dispatch(GET_PACKAGE_INFO, { packageName: value });
    },
  },
  emits: ['update:model-value'],
  methods: {
    updateModelValue(value) {
      this.$emit('update:model-value', value);
    }
  },
}
</script>

<style lang="scss">
  .package-dialog {
    &__avatar {
      width: 20px;
      height: 20px;
    }
  }
</style>
