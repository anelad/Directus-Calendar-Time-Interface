<template>
  <div :class="{ inactive: readonly }">
    <flat-pickr class="form-control" :config="configs" :value="value" @input="$emit('input', $event)"></flat-pickr>
  </div>
</template>

<script>
import flatPickr from "vue-flatpickr-component";
import mixin from "@directus/extension-toolkit/mixins/interface";
import format from "date-fns/format";

import "./calendar.css";

export default {
  name: "InterfaceCalendarTime",
  components: {
    flatPickr
  },
  mixins: [mixin],
  computed: {
    configs() {
      return {
        time_24hr: true,
        enableTime: true,
        inline: true,
        minDate: this.options.min,
        maxDate: this.options.max,
        dateFormat: "Y-m-d H:i:S",
        onReady() {
          this.showTimeInput = true;
        }
      };
    }
  },
  created() {
    if (this.options.defaultDatetime && !this.value) {
      this.$emit("input", format(new Date(), "yyyy-MM-dd HH:mm:ss"));
    }
  }
};
</script>

<style lang="scss" scoped>
.inactive {
  pointer-events: none;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
</style>
