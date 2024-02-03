# Next.js 13 Routing

- to create route you have to create directory path that represents the route and put **page.js** inside it
  for example if you want to create rout `a/b` you need to create this directory strucutre `a/b/page.js`

- Pages are **server components** by default

- you can have a _layout.js_ file in the same directory as the _page.js_ when the route is requestd the _layout.js_
  will be rendered first then the _page.js_ will be rendered inside it as child props

- you can use the `<Link href="/url">` component to navigate, or use the `useRouter` hook to programmatically navigate

- when a `<Link>` component comes into user's view, next will prefetch the page that it "links"
  to in the background and cache it for later use, you can explicitly prefetch a page using router.prefecth()
