---
highlight: github
---

## 对比前提

目前 Tailwind css 的 ⭐️ 是**79.2k**,而 Unocss 的 ⭐️ 是**15.2k**

本次对比主要是在两个项目打包大小和浏览器体验评分上做简单对比，仅作参考。

## 两个框架的优势

**Tailwind CSS:**

• **工具优先框架:** 提供一套实用工具类，可以直接在标记中设计样式。

• **定制化:** 通过配置文件进行广泛的定制。

• **性能:** 通过清除未使用的样式来减少最终的 CSS 大小。

• **生态系统:** 拥有丰富的插件生态和广泛的社区支持。

**Unocss:**

• **按需生成 CSS:** 根据模板中使用的类名即时生成样式。

• **性能:** 最小化初始 CSS 负载，仅生成所需的样式。

• **定制化:** 通过预设和灵活的配置进行高度定制。

• **集成:** 专为与各种框架无缝协作设计，包括对 Vue.js 的一流支持。

## 测试环境

*vue@3.4.21, vite@.2.0, tailwindcss@3.4.3, unocss@0.60.3*

## 项目初始化

### Tailwind css

创建 Vue3 项目

```bash
npm init vite@latest tailwind-vue --template vue
```

配置 Tailwind CSS

```bash
# 安装 Tailwind CSS 及其依赖
cd tailwind-vue
pnpm install tailwindcss postcss autoprefixer

# 初始化 Tailwind CSS
pnpx tailwindcss init -p
```

在 tailwind.config.js 中：

```js
module.exports = {
	purge: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
	darkMode: false, // or 'media' or 'class'
	theme: {
		extend: {},
	},
	variants: {
		extend: {},
	},
	plugins: [],
}
```

在 src/assets/tailwind.css 中：

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

在 main.js 中引入 Tailwind CSS：

```js
import { createApp } from 'vue'
import App from './App.vue'
import './assets/tailwind.css'

createApp(App).mount('#app')
```

### Unocss

创建 Vue3 项目

```bash
npm init vite@latest unocss-vue --template vue
```

配置 Unocss

```bash
# 安装 Unocss 及其依赖
cd unocss-vue
npm install @unocss/core @unocss/vite unocss
```

在 vite.config.js 中配置 Unocss 插件：

```js
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import Unocss from 'unocss/vite'

export default defineConfig({
	plugins: [vue(), Unocss()],
})
```

在 src/main.js 中引入 Unocss：

```js
import { createApp } from 'vue'
import App from './App.vue'
import 'uno.css'

createApp(App).mount('#app')
```

在项目根目录下创建 unocss.config.js：

```js
import { defineConfig } from 'unocss'

export default defineConfig({
	// 这里可以添加自定义配置
})
```

## 组件内容

在两个项目的 src/components 目录下创建的 HelloWorld.vue 组件：

Tailwind css

```js
<template>
  <div class="bg-white py-24 sm:py-32">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl lg:mx-0">
        <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">From the blog</h2>
        <p class="mt-2 text-lg leading-8 text-gray-600">Learn how to grow your business with our expert advice.</p>
      </div>
      <div
        class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-x-8 gap-y-16 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">
        <article v-for="post in posts" :key="post.id" class="flex max-w-xl flex-col items-start justify-between">
          <div class="flex items-center gap-x-4 text-xs">
            <time :datetime="post.datetime" class="text-gray-500">{{ post.date }}</time>
            <a :href="post.category.href"
              class="relative z-10 rounded-full bg-gray-50 px-3 py-1.5 font-medium text-gray-600 hover:bg-gray-100">{{
                post.category.title }}</a>
          </div>
          <div class="group relative">
            <h3 class="mt-3 text-lg font-semibold leading-6 text-gray-900 group-hover:text-gray-600">
              <a :href="post.href">
                <span class="absolute inset-0" />
                {{ post.title }}
              </a>
            </h3>
            <p class="mt-5 line-clamp-3 text-sm leading-6 text-gray-600">{{ post.description }}</p>
          </div>
          <div class="relative mt-8 flex items-center gap-x-4">
            <img :src="post.author.imageUrl" alt="" class="h-10 w-10 rounded-full bg-gray-50" />
            <div class="text-sm leading-6">
              <p class="font-semibold text-gray-900">
                <a :href="post.author.href">
                  <span class="absolute inset-0" />
                  {{ post.author.name }}
                </a>
              </p>
              <p class="text-gray-600">{{ post.author.role }}</p>
            </div>
          </div>
        </article>
      </div>
    </div>
  </div>
</template>

<script setup>
const posts = [
  {
    id: 1,
    title: 'Boost your conversion rate',
    href: '#',
    description:
      'Illo sint voluptas. Error voluptates culpa eligendi. Hic vel totam vitae illo. Non aliquid explicabo necessitatibus unde. Sed exercitationem placeat consectetur nulla deserunt vel. Iusto corrupti dicta.',
    date: 'Mar 16, 2020',
    datetime: '2020-03-16',
    category: { title: 'Marketing', href: '#' },
    author: {
      name: 'Michael Foster',
      role: 'Co-Founder / CTO',
      href: '#',
      imageUrl:
        'https://images.unsplash.com/photo-1519244703995-f4e0f30006d5?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
  },

  // More posts...
]
</script>
```

unocss 的 Helloword.vue

```js
<template>
  <div class="bg-white py-24 sm:py-32">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl lg:mx-0">
        <h2 class="text-3xl font-bold tracking-tight text-gray-900 sm:text-4xl">From the blog</h2>
        <p class="mt-2 text-lg leading-8 text-gray-600">Learn how to grow your business with our expert advice.</p>
      </div>
      <div
        class="mx-auto mt-10 grid max-w-2xl grid-cols-1 gap-x-8 gap-y-16 border-t border-gray-200 pt-10 sm:mt-16 sm:pt-16 lg:mx-0 lg:max-w-none lg:grid-cols-3">
        <article v-for="post in posts" :key="post.id" class="flex max-w-xl flex-col items-start justify-between">
          <div class="flex items-center gap-x-4 text-xs">
            <time :datetime="post.datetime" class="text-gray-500">{{ post.date }}</time>
            <a :href="post.category.href"
              class="relative z-10 rounded-full bg-gray-50 px-3 py-1.5 font-medium text-gray-600 hover:bg-gray-100">{{
                post.category.title }}</a>
          </div>
          <div class="group relative">
            <h3 class="mt-3 text-lg font-semibold leading-6 text-gray-900 group-hover:text-gray-600">
              <a :href="post.href">
                <span class="absolute inset-0" />
                {{ post.title }}
              </a>
            </h3>
            <p class="mt-5 line-clamp-3 text-sm leading-6 text-gray-600">{{ post.description }}</p>
          </div>
          <div class="relative mt-8 flex items-center gap-x-4">
            <img :src="post.author.imageUrl" alt="" class="h-10 w-10 rounded-full bg-gray-50" />
            <div class="text-sm leading-6">
              <p class="font-semibold text-gray-900">
                <a :href="post.author.href">
                  <span class="absolute inset-0" />
                  {{ post.author.name }}
                </a>
              </p>
              <p class="text-gray-600">{{ post.author.role }}</p>
            </div>
          </div>
        </article>
      </div>
    </div>
  </div>
</template>

<script setup>
const posts = [
  {
    id: 1,
    title: 'Boost your conversion rate',
    href: '#',
    description:
      'Illo sint voluptas. Error voluptates culpa eligendi. Hic vel totam vitae illo. Non aliquid explicabo necessitatibus unde. Sed exercitationem placeat consectetur nulla deserunt vel. Iusto corrupti dicta.',
    date: 'Mar 16, 2020',
    datetime: '2020-03-16',
    category: { title: 'Marketing', href: '#' },
    author: {
      name: 'Michael Foster',
      role: 'Co-Founder / CTO',
      href: '#',
      imageUrl:
        'https://images.unsplash.com/photo-1519244703995-f4e0f30006d5?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
    },
  },
  // More posts...
]
</script>
```

## 打包对比

Tailwind css build 后的结果

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d80eaf76f5e7489588f8b215c66abf2b~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1062&h=264&s=67735&e=png&b=43444f)

Unocss build 后的结果

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a5002aafd80643ea824eee476d6b8845~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1072&h=302&s=77905&e=png&b=43444f)

> Unocss 的打包后 css 的体积是 Tailwind 的 65% 左右

## Lighthouse 对比

两个项目同时 build 后，在 Edge 浏览器 v126 无痕模式环境下测试 Lighthouse 的评分基本一致（桌面和移动端）。

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/566f23b648254c8d9762402123214594~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=2084&h=1116&s=168741&e=png&b=fdfdfd)

## 测试内容源码

> Todo：测试复杂项目里两个框架使用情况的对比。
