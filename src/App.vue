<template>
  <div id="app">
    <AddCalendarButton
      start="2021/10/15 09:30"
      end="2021/10/15 09:40"
      title="标题：领导致辞--加拿大驻重庆总领事馆领导"
      description="描述：领导致辞--加拿大驻重庆总领事馆领导"
      location="地点：成都"
      organizerEmail="asdhgjsdg@123123.com"
    ></AddCalendarButton>
  </div>
</template>

<script>
import AddCalendarButton from "./components/AddCalendarButton";

export default {
  name: "App",
  components: {
    AddCalendarButton,
  },
};
</script>
