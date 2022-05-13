# Add Calendar Button Vue 2

## 安装

```
npm install add-calendar-button-vue2
```

### 使用示例

```vue
<template>
  <AddCalendarButton
    start="2022/05/12 12:00"
    end="2022/05/14 12:00"
    title="标题"
    timezone=""
    description="描述"
    location="地点"
  >
    添加到日历
  </AddCalendarButton>
</template>

<script>
import AddCalendarButton from "add-calendar-button-vue2";

export default {
  name: "Demo",
  components: {
    AddCalendarButton,
  },
};
</script>
```
