<template>
  <div>
    <h3 class="configure-context-title">Options</h3>

    <div class="configure-design-item">
      <div class="configure-design-text">Direction:</div>
      <div class="configure-options">
        <div class="configure-radio">
          <label>
            <input v-model="isReverse" type="radio" class="uk-radio" name="editor-direction" :value="false" />Upward
          </label>
        </div>
        <div class="configure-radio">
          <label>
            <input v-model="isReverse" type="radio" class="uk-radio" name="editor-direction" :value="true" />Downward
          </label>
        </div>
      </div>
    </div>
    <div class="configure-design-item">
      <div class="configure-design-text">Freeze Highlight:</div>
      <div class="configure-options">
        <div class="configure-radio">
          <label>
            <input v-model="isHighlightedFreeze" type="radio" class="uk-radio" name="editor-highlighted-freeze" :value="true" />
            <span class="configure-radio-text">On</span>
          </label>
        </div>
        <div class="configure-radio">
          <label>
            <input v-model="isHighlightedFreeze" type="radio" class="uk-radio" name="editor-highlighted-freeze" :value="false" />
            <span class="configure-radio-text">Off</span>
          </label>
        </div>
      </div>
    </div>
    <div class="configure-design-item">
      <div class="configure-design-text-long">Simultaneous Threshold(msec):</div>
      <div class="configure-options">
        <input v-model.number="simultaneousThreshold" type="number" min="-1" max="1000" step="1" class="uk-input uk-form-small" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "ConfigureDesign",
  data() {
    return {
      simultaneousThreshold: 0,
    };
  },
  computed: {
    isReverse: {
      get(): boolean {
        const isReverseStr: string = localStorage.getItem("isReverse") ?? "false";
        return JSON.parse(isReverseStr);
      },

      set(newValue: boolean): boolean {
        localStorage.setItem("isReverse", JSON.stringify(newValue));
        return newValue;
      },
    },

    isHighlightedFreeze: {
      get(): boolean {
        const isHighlightedFreezeStr: string = localStorage.getItem("isHighlightedFreeze") ?? "true";
        return JSON.parse(isHighlightedFreezeStr);
      },

      set(newValue: boolean): boolean {
        localStorage.setItem("isHighlightedFreeze", JSON.stringify(newValue));
        return newValue;
      },
    },
  },
  watch: {
    simultaneousThreshold(newValue) {
      localStorage.setItem("simultaneousThreshold", JSON.stringify(newValue));
    },
  },
  mounted() {
    this.simultaneousThreshold = JSON.parse(localStorage.getItem("simultaneousThreshold") ?? "30");
  },
});
</script>
