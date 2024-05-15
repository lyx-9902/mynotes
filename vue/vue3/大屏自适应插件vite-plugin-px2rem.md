# vite-plugin-px2rem

https://github.com/ch1ny/vite-plugin-px2rem/blob/HEAD/README-zh_CN.md

## 介绍

一个支持将你的样式表中的 `px` 转换成 `rem` 的 `vite` 插件。

支持 `css`、`less` 以及 `sass/scss`。

> 不支持对 `js/ts` 文件内部的代码进行转换。

写在标签内的样式，不起作用。

```
# npm
npm install vite-plugin-px2rem --save-dev
```

在 vite 中使用:

```
// vite.config.ts
import { defineConfig } from 'vite';
import { px2rem } from 'vite-plugin-px2rem';

// https://vitejs.dev/config/
export default defineConfig({
	plugins: [
		px2rem({
			width: 750,
			rootFontSize: 16,
		}),
	],
});
```

