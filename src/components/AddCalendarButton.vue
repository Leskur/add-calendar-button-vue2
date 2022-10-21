<template>
  <div title="Add to Calendar" class="addeventatc" v-bind="$attrs">
    <slot>添加到日历</slot>
    <span class="start">{{ start }}</span>
    <span v-if="end" class="end">{{ end }}</span>
    <span v-if="timezone" class="timezone">{{ timezone }}</span>
    <span class="title">{{ title }}</span>
    <span v-if="description" class="description">{{ description }}</span>
    <span v-if="location" class="location">{{ location }}</span>
  </div>
</template>

<script>
let loading = false;

export default {
  name: "AddCalendarButton",
  props: {
    start: {
      type: String,
      required: true,
    },
    end: String,
    timezone: {
      type: String,
      default: Intl.DateTimeFormat().resolvedOptions().timeZone,
    },
    title: {
      type: String,
      required: true,
    },
    description: String,
    location: String,
    settings: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  created() {
    if (!this.hasJsInHead()) {
      this.addJsInHead();
    }
  },
  mounted() {
    if (window.addeventatc) {
      window.addeventatc.generate();
    }
  },
  methods: {
    hasJsInHead() {
      return document.head.querySelector(
        "script[src='https://cdn.addevent.com/libs/atc/1.6.1/atc.min.js']"
      );
    },
    addJsInHead() {
      if (loading) {
        return false;
      }
      loading = true;

      const script = document.createElement("script");
      script.src = "https://cdn.addevent.com/libs/atc/1.6.1/atc.min.js";
      script.setAttribute("async", "");
      script.setAttribute("defer", "");
      script.onload = () => {
        loading = false;
        window.addeventatc.settings(
          Object.assign(
            {
              appleical: { show: true, text: "Apple Calendar" },
              google: { show: true, text: "Google <em>(online)</em>" },
              office365: { show: true, text: "Office 365 <em>(online)</em>" },
              outlook: { show: true, text: "Outlook" },
              outlookcom: { show: true, text: "Outlook.com <em>(online)</em>" },
              yahoo: { show: true, text: "Yahoo <em>(online)</em>" },
            },
            this.settings
          )
        );
        const style = document.createElement("style");
        style.type = "text/css";
        style.innerText = ".addeventatc{visibility:visible !important;}";
        setTimeout(() => {
          document.head.appendChild(style);
        }, 300);
      };
      document.head.appendChild(script);
    },
    toLine(name) {
      console.log(name);
      return name.replace(/([A-Z])/g, "_$1").toLowerCase();
    },
  },
};
</script>
