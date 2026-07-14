<template>
  <AppLayout>
    <div class="mx-auto max-w-5xl px-4 py-8">
      <!-- 标题 -->
      <div class="mb-8 text-center">
        <h1 class="text-3xl font-bold text-gray-900 dark:text-white">
          {{ t('guide.title') }}
        </h1>
        <p class="mt-2 text-gray-600 dark:text-gray-400">
          {{ t('guide.description') }}
        </p>
      </div>

      <!-- 图片展示区域 -->
      <div class="space-y-6">
        <div
          v-for="(guide, index) in guides"
          :key="index"
          class="overflow-hidden rounded-2xl border border-gray-200 bg-white shadow-sm transition-shadow hover:shadow-md dark:border-dark-700 dark:bg-dark-800"
        >
          <!-- 图片标题 -->
          <div class="border-b border-gray-200 px-6 py-4 dark:border-dark-700">
            <h2 class="text-lg font-semibold text-gray-900 dark:text-white">
              {{ guide.title }}
            </h2>
          </div>

          <!-- 图片内容 -->
          <div class="p-6">
            <img
              :src="guide.image"
              :alt="guide.title"
              class="w-full rounded-lg"
              @error="onImageError"
            />
          </div>
        </div>

        <!-- 如果没有图片，显示提示 -->
        <div
          v-if="guides.length === 0"
          class="rounded-2xl border-2 border-dashed border-gray-300 p-12 text-center dark:border-dark-600"
        >
          <Icon name="document" size="xl" class="mx-auto text-gray-400 dark:text-gray-500" />
          <h3 class="mt-4 text-lg font-medium text-gray-900 dark:text-white">
            {{ t('guide.noGuides') }}
          </h3>
          <p class="mt-2 text-sm text-gray-500 dark:text-gray-400">
            {{ t('guide.noGuidesDescription') }}
          </p>
        </div>
      </div>
    </div>
  </AppLayout>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useI18n } from 'vue-i18n'
import AppLayout from '@/components/layout/AppLayout.vue'
import Icon from '@/components/icons/Icon.vue'

const { t } = useI18n()

// 用户指南配置
// 将你的图片放在 frontend/public/guides/ 文件夹中
// 然后在这里添加图片路径和标题
const guides = ref([
  {
    title: '使用指南 1',
    image: '/guides/guide-1.png'
  },
  {
    title: '使用指南 2', 
    image: '/guides/guide-2.png'
  },
  {
    title: '使用指南 3',
    image: '/guides/guide-3.png'
  },
  {
    title: '使用指南 4',
    image: '/guides/guide-4.png'
  },
  {
    title: '使用指南 5', 
    image: '/guides/guide-5.png'
  },
  {
    title: '使用指南 6',
    image: '/guides/guide-6.png'
  }
  // 继续添加更多指南...
])

const onImageError = (event: Event) => {
  const img = event.target as HTMLImageElement
  console.warn('Failed to load image:', img.src)
}
</script>
