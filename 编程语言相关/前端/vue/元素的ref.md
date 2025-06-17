```vue
<script setup>
import { ref,onMounted } from 'vue'

const target=ref(null)

</script>

<template>
	<div ref="target" class=""></div>
</template>
```

>ref的变量名(target) 与div中的的ref值(target) 相同时，可以自动获取到dom中的同名div元素
