### NextJS-Cheats-Sheet

#### 1) Create a Next.js App
```javascript
npx create-next-app {app_name}
```

#### 2) Start dev server
```javascript
npm run dev
```

#### 3) Folders:
- pages (react component file, get render as page, file based routing)

#### 4) Create dynamic pages & extracting dynamic query string data
- create pages/news/[newsId].js 
- extract newsId with
```javascript
  import { useRouter } from 'next/router';

  const router = userRouter();
  const id = router.query.newsId;
```

#### 5) Linking between pages
```javascript
  import Link from 'next/link';

  function MyPage() {
    return (
      <Link href='page_to_page'>Some text here</Link>
    );
  }
```

#### 6) Global settings in Next.js at pages/_app.js
- persisting layout between pages
- keeping state when navigating pages
- custom error handling uisng 'componentDidCatch'
- inject additional data into pages
- add global CSS

#### 7) Programmatic navigation
```javascript
  import { useRouter } from 'next/router';

  useRouter().push('path_to_page');
```

#### 8) Build for production
```javascript
  npm run build
```

#### 9) Pre-rendering (Pre-rendering code run at build time/server side is not expose to client)
- static generation (generate at build time)
- server-side rendering (generate at each request)