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
      <Link href='path_to_page'>Some text here</Link>
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

#### 9a) Static generation (functions: getStaticProps, getStaticPaths)
```javascript
  export async function getStaticProps(){
    //fetch data from an API operation
    return {
      props: { 'page_props' },
      // incremental build every 10 seconds if there is incoming request
      revalidate: 10
    }
  }
```
```javascript
  //example code for pages/[newsId].js
  export async function getStaticPaths(){
    //fetch data from an API to get values for newsId
    return {
      paths: [
        { params: { newsId: fetchResult[0] }},
        { params: { newsId: fetchResult[1] }}
        ],
      // possible fallback options: 1) false 2) true 3) 'blocking'
      // falseback=false: path not defined will be 404
      fallback: false
    }
  }
```
#### 10) Server side rendering (functions: getInitialProps, getServerSideProps)
```javascript
  export async function getServerSideProps(context){
    //fetch data from an API
    //express's req, res: context.req / context.res
    return {
      props: 'your_page_data'
    }
  }
```

#### 11) API routes
- all files created at /pages/api will receive req, res params
```javascript
  // POST /pages/api/new-meetup.js
  function handler(req, res){
    if(req.method === 'POST'){
      const data = req.body;
    }
    // return
    res.status(201).json(data);
  }

  export default handler;
```