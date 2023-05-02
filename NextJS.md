# NextJS


### Features
- Built in webpack
- Built in CSS, SCSS, SASS support
- CSS Modules support using the [name].module.css (automatically creating a unique class names)


### API

<table width="100%">
<tbody >
    <tr>
        <td>'next/image'</td>
        <td>v10+</td>
        <td>
            • images are automatically lazy-loaded, meaning they're only rendered when the user is close to seeing the image. <br/> 
            • automatically generate smaller sizes through built-in Image Optimization<br/>
            • automatically serves the images in modern image formats like WebP, which is about 30% smaller than JPEG, if the browser supports it.<br/>  
            • Instead of optimizing images at build time, Next.js 10 optimizes images on-demand, as users request them.<br/>
        </td>
    </tr>
    <tr>
        <td>'next/head'</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>'next/link'</td>
        <td></td>
        <td>
            • v10+ Automatic Resolving of href<.. href="/categories/[slug]" as="/categories/books"><br/> 
        </td>
    </tr>
    <tr>
        <td>'next/router'</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>'next/dynamic'</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>'next/constants'</td>
        <td></td>
        <td>{ PHASE_DEVELOPMENT_SERVER } </td>
    </tr>
    <tr>
        <td>'next/config'</td>
        <td></td>
        <td> </td>
    </tr>


</tbody>
</table>

## Rendering

Next.JS supports two types of pre-rendering.
 
We recommend using Static Generation over Server-side Rendering for performance reasons.

**Static Generation** − This method generates the HTML page at build time. This pre-rendered HTML is sent on each request. This method is useful for marketing websites, blogs, e-commerce products listing wesites, helps, documentation websites.
If a page uses Static Generation, the page HTML is generated at build time. That means in production, the page HTML is generated when you run next build . This HTML will then be reused on each request.


**Server Side Generation** − This method generates the HTML page on each request. This method is suitable when an html page contents can vary with each request.
If a page uses Server-side Rendering, the page HTML is generated on each request.

---

#### Static Generation Without Data
Static generation can be done without data in which case, HTML pages will be ready without need to prefetch the data and then start rendering. Data can be fetched later or on request.

#### Static Generation With Data
Static generation can be done with data in which case, HTML pages will not be ready until data is fetched, as HTML may be dependent on data.


| Method             | Ver.|                                                     |
|--------------------|-----|-----------------------------------------------------|
| getInitialProps    |     | runs for every request (initial-on server, then on client side )    |
| getServerSideProps | 9.3 | runs for every request, server-side only  (analytical charts)          |
| getStaticProps     | 9.3 | runs at build time in production and runs for every request in dev mode. (articles)  |



### getInitialProps
```javascript
//• getInitialProps will disable Automatic Static Optimization.
//• For the initial page load, getInitialProps will run on the server only, then run on the client when used 'next/link' component or by using 'next/router'
class ShopPage extends Component {
    static async getInitialProps({pathname, query, asPath, req, res, err}) {
        const shop = axios.get('....');
        return { shop:shop.data };
    }
}
```
```javascript
function Page({ stars }) {
    return <div>Next stars: {stars}</div>
}

Page.getInitialProps = async (ctx) => {
    const res = await fetch('https://api.github.com/repos/vercel/next.js')
    const json = await res.json()
    return { stars: json.stargazers_count }
}
```


### getStaticProps (ver. 9.3+)

```javascript
function Blog({ posts }) {
    return (...)
}
// This function gets called at build time on server-side.
// It won't be called on client-side, so you can even do
// direct database queries.  
export async function getStaticProps() {
  // Call an external API endpoint to get posts. You can use any data fetching library
  const res = await fetch('https://.../posts');
  const posts = await res.json();

  // By returning { props: posts }, the Blog component will receive `posts` as a prop at build time
  return {
    props: { posts, },
  }
}

export default Blog;
```

### getServerSideProps (ver. 9.3+)
```javascript
//You should not use fetch() to call an API route in getServerSideProps. Instead, directly import the logic used inside your API route.

export async function getServerSideProps({params, req, res, query, preview, previewData, resolvedUrl, locale, locales, defaultLocale, }) {
  
    return {
        props: {}, // will be passed to the page component as props
        redirect:{destination: '/', permanent: false,} //optional
  }
}
```


## Link
```javascript
//v10+ no need of as
<Link href="/posts/first-post">
```

## Images
```javascript
import Image from 'next/image'

<Image
    src="/images/profile.jpg" // Route of the image file
    height={144} // Desired size with correct aspect ratio
    width={144} // Desired size with correct aspect ratio
    alt="Your Name"
/>
```

## Head
Allows to modify the <head> of a page.

```javascript
import Head from 'next/head';

export default function FirstPost() {
    return (<>
            <Head>
                <title>First Post</title>
            </Head>
            <h1>First Post</h1>
        </>)
}

```



---

## Next Config
```javascript
// next.config.js

module.exports = {
    basePath: '/store',
    poweredByHeader: false,//optional, Disable "x-powered-by" header
    generateEtags: false,//optional, disable etags 

    distDir: 'build',//optional, set a custum build dir
    
    assetPrefix: isProd ? 'https://cdn.mydomain.com' : '',
    compress: true,//optional, true by default
    
    //environment variables
    env: {customKey: 'my-value'},  
    
    //Runtime configs
    // Runtime configuration won't be available to any page (or component in a page) without getInitialProps.
    serverRuntimeConfig: {
        // Will only be available on the server side
        mySecret: 'secret',
        secondSecret: process.env.SECOND_SECRET, // Pass through env variables
    },
    publicRuntimeConfig: {
        // Will be available on both server and client
        staticFolder: '/static',
    },
}
```


### Rewrites
```javascript
module.exports = {
  async rewrites() {
    return [
      // we need to define a no-op rewrite to trigger checking
      // all pages/static files before we attempt proxying
      {
        source: '/:path*',
        destination: '/:path*',
      },
      {
        source: '/:path*',
        destination: `https://proxy.example.com/:path*`,
      },
    ]
  },
}
```
### Redirects
```javascript
module.exports = {
  async redirects() {
    return [
      {
        source: '/about',
        destination: '/',
        permanent: true,
      },
    ]
  },
}
```

## Custom Headers 
```javascript
module.exports = {
  async headers() {
    return [{
        source: '/about',
        headers: [
          {key: 'x-custom-header', value: 'my custom header value'},
        ],
      }]
  },
}
```
---
---

### NextJS CLI
```javascript
npx next -h
```


---
### Next Router
```javascript
import { withRouter, useRouter } from 'next/router';

//useRouter is a React Hook, meaning it cannot be used with classes

```
