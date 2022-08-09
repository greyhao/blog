## Next.js

Next.js 是一个 React 开发框架

* 直观、基于页面的路由
* 预渲染，支持页面级的 SSC（静态生成）和 SSR（服务器渲染）
* 自动拆分代码，提升页面加载速度
* 经过优化的预取功能的客户端路由
* 内置 CSS 和 Sass 的支持，并支持任何 CSS-in-JS 库
* 开发环境支持快速刷新
* 利用 Serverless Functions 及 API 路由构建 API 功能
* 完全可扩展



###项目结构

![image-20220727160731447](https://tva1.sinaimg.cn/large/e6c9d24ely1h4ljsgu9d7j20l80ymmzi.jpg)



* `pages` 所有页面均在改目录下
  * `api`  API 接口目录
  * `posts` 自定义路径的目录
  * `_app.js`  设置全局样式的 js 文件
  * `404.js` 自定义 404 页面
  * `index.js` 首页，对应路径：域名/

* `public`  静态资源
  * `image` 图片
* `styles`  css 样式
  * `global.css` 全局样式
  * `utils.module.css` 控件样式，后缀 .module.css 不可改



###创建应用

`npx create-next-app name-xx`  // 



```shell
npx create-next-app nextjs-blog --use-npm --example "https://github.com/vercel/next-learn/tree/master/basics/learn-starter"
```

// --example 参数指定使用模版







### 运行

`npm run dev`



###路由

页面都在 `app/pages/` 目录下

​	/pages/index.js 请求时对应路径 /

​	/pages/about/me.js 请求时对应路径 /about/me



 内部页面跳转使用 Link，外部页面使用 a 标签

```react
import Link from "next/link";

<Link href="/">
	<a>Back to home</a>
</Link>
```



Link 使用 JavaScript 进行页面转换。



### 资源

资源放置路径：`app/public/images/` 



####图像

使用 next/image，该控件用户请求时优化图像，

```react
import Image from "next/image";

<Image src="/images/unnamed.png" height={144} width={144} alt="Img" />
```



#### Head

设置 title

```react
import Head from "next/head";

<Head>
	<title>First Post</title>
</Head>
```



#### 加载第三方脚本

引用 js sdk

```react
import Script from "next/script";

<Script
	src="https://connect.facebook.net/en_US/sdk.js"
	strategy="lazyOnload"
	onLoad={() =>
		console.log(`script loaded correctly, window.FB has been populated`)
	}
/>
```



#### 布局控件

```react
export default function Layout({ children }) {
  return <div>{children}</div>;
}
```





#### CSS

Next.js 内置了对 [styled-jsx](https://github.com/vercel/styled-jsx) 的支持，可以在 React 控件中写 CSS，并且不会影响其他控件。

```react
<style jsx>{`
	// css 
`}</style>
```



CSS 模块文件名必须以 `.module.css` 结尾

```css
/* layout.module.css */
/* 定义 CSS 文件  */
.container {
  max-width: 36rem;
  padding: 0 1rem;
  margin: 3rem auto 6rem;
}
```



```react
// layout.js 
// 引入 css 文件
import styles from "./layout.module.css";

export default function Layout({ children }) {
  return <div className={styles.container}>{children}</div>;
}
```



会自动生成独特的 className



##### 全局样式

创建文件 `/pages/_app.js`，将全局样式文件导入到 _app.js 中。首次创建 _app.js 文件需要重新启动服务。并且只有 _app.js 可以导入全局样式



### 预渲染

两种方式

* 静态生成
  * 在构建时生成 HTML，然后在每个请求上重用预呈现的 HTML
  * 更快
  * 非频繁需要更新的页面
  * 请求数据：`getStaticProps`
* 服务器端渲染 
  * 在每个请求上生成 HTML
  * 渲染的页面始终是新的
  * 每次请求都会重新生成
  * 请求数据：`getServerSideProps`

可以为每个页面设置不同的预渲染方式



### 定义 html 属性

在文件 `pages/_document.js` 中设置



### 第三方库

#### 数据库

1. 设置 Prisma 和连接数据库

2. 安装 `npm install prisma --save-dev`

初始化设置 `npx prisma init` // 1. 创建 prisma/schema.prisma 文件，在这个文件中连接数据库和定义表 2. 创建 .env 文件，该文件用来配置数据库连接 ULR 和其他敏感信息

3. 在 .env 文件中设置 DATABASE_URL 的实际值

4. 在 schema.prisma 文件中定义数据表及连接变量

5. 在数据库中创建表 `npx prisma db push`

6. 打开数据库 GUI `npx prisma studio` // 可以查询、添加、删除数据

7. 安装 prisma client  `npm install @prisma/client`

8. 生成 prisma schema  `npx prisma generate` // 只要 scheme.prisma  文件发生改变都需要执行改命令

9. 创建 PrismaClient 单例对象

   ```react
   // lib/prisma.ts
   import { PrismaClient } from '@prisma/client';
   
   let prisma: PrismaClient;
   
   if (process.env.NODE_ENV === 'production') {
     prisma = new PrismaClient();
   } else {
     if (!global.prisma) {
       global.prisma = new PrismaClient();
     }
     prisma = global.prisma;
   }
   
   export default prisma;
   ```

   

10. 操作语句

    ```react
    
    ```



#### OAuth 登陆 

使用 NextAuth.js

1. 安装 `npm install next-auth@4 @next-auth/prisma-adapter`
2. 创建 GitHub OAuth application



### 部署

使用 [vercel](https://vercel.com/dashboard) 进行部署，可以自行配置动态参数等。

关联 GitHub，提交代码后自动部署。



数据库 PosgtreSQL，使用 [Heroku](https://data.heroku.com/) 的免费版本。



原文

[How to Build a Fullstack App with Next.js, Prisma, and PostgreSQL](https://vercel.com/guides/nextjs-prisma-postgres#step-2:-set-up-prisma-and-connect-your-postgresql-database)