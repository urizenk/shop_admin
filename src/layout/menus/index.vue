<template>
  <div class="menu">
    <template v-for="(item, index) in menuList" :key="item.path">
      <template v-if="!item.children">
        <el-menu-item
          v-if="!item.meta.hidden"
          :index="item.path"
          @click="goRoute"
        >
          <el-icon><component :is="item.meta.icon"></component></el-icon>
          <template #title>
            <span>{{ item.meta.title }}</span>
          </template>
        </el-menu-item>
      </template>
      <template v-if="item.children && item.children.length == 1">
        <el-menu-item
          v-if="!item.meta.hidden"
          :index="item.children[0].path"
          @click="goRoute"
        >
          <el-icon>
            <component :is="item.children[0].meta.icon"></component>
          </el-icon>
          <template #title>
            <span>{{ item.children[0].meta.title }}</span>
          </template>
        </el-menu-item>
      </template>
      <template v-if="item.children && item.children.length > 1">
        <el-sub-menu
          v-if="!item.meta.hidden"
          :index="item.path"
          :key="index"
          @click="goRoute"
        >
          <template #title>
            <el-icon><component :is="item.meta.icon"></component></el-icon>
            <span>{{ item.meta.title }}</span>
          </template>
          <menus :menuList="item.children"></menus>
        </el-sub-menu>
      </template>
    </template>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, toRefs, onMounted, defineProps } from 'vue'
import { useRouter } from 'vue-router'
defineProps(['menuList'])

let $router = useRouter()

const goRoute = (vc: any) => {
  $router.push(vc.index)
}
</script>
<script lang="ts">
export default {
  name: 'menus',
}
</script>
<style scoped lang="scss">
.menu {
  color: rgb(255, 255, 255);
}
</style>
