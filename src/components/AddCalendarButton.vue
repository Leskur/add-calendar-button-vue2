<template>
  <div title="Add to Calendar" class="addeventatc">
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
  },
  created() {
    if (!this.hasJsInHead()) {
      this.addJsInHead();
    } else {
      window.addeventatc.generate()
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
      script.onload = function () {
        loading = false;
        window.addeventatc.settings({
          appleical: { show: true, text: "Apple Calendar" },
          google: { show: true, text: "Google <em>(online)</em>" },
          office365: { show: true, text: "Office 365 <em>(online)</em>" },
          outlook: { show: true, text: "Outlook" },
          outlookcom: { show: true, text: "Outlook.com <em>(online)</em>" },
          yahoo: { show: true, text: "Yahoo <em>(online)</em>" },
        });
        const style = document.createElement("style");
        style.type = "text/css";
        style.innerText = ".addeventatc{visibility:visible !important;}";
        document.head.appendChild(style);
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

<style scoped>
.addeventatc {
  visibility: hidden;
  padding: 7px 11px 7px 34px;
  font-size: 13px;
  line-height: 18px;
  box-sizing: border-box;
  border-radius: 4px;
}

.addeventatc:hover {
  font-size: 13px;
}

.addeventatc /deep/ .addeventatc_icon {
  width: 16px;
  height: 16px;
  top: 8px;
  left: 10px;
  background-size: 16px;
}

/*/deep/ .addeventatc_dropdown .copyx {*/
/*  display: none;*/
/*}*/
</style>
