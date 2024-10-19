## Frontend

<details>
<summary>Advice</summary>
<br>

> ### **`Advice`** :
**`CAUTION :`** Don't waste much time in HTML and CSS as you will learn them along the way, focus more on the basics of JavaScript. <br>
**`ADVICE :`** You will definitely always feel underconfident about HTML CSS JS but after making some basic projects move on to React.js as you will learn them along the way,

</details>


<details>
<summary>Resources</summary>
<br>

> ### **`Resources`** :
- Vite + Typescript : https://www.youtube.com/watch?v=665UnOGx3Pg
- Next + Typescript : https://www.youtube.com/watch?v=TPACABQTHvM
- <details>
  <summary>Vite + Typescript + ShadcnUI :</summary>
  <br>

    Docs: [Vite - shadcn/ui](https://ui.shadcn.com/docs/installation/vite)
    
     - Step 1 :
    Run below command to initialize and configure components.json
    go for defaults in options ->
    ```bash
    npx shadcn-ui@latest init
    ```
    
    - Step 2 :
    Resolve import paths for library :
    > NOTE : We have to resolve path for all `vite`, `tailwind` and `typescript` 
    ```javascript
    // tailwind.config.js ::
    
    content: [
        "./index.html",
        './pages/**/*.{ts,tsx}',
        './@/components/**/*.{ts,tsx}',
        './app/**/*.{ts,tsx}',
        './src/**/*.{ts,tsx}',
      ],
    ```
    ---
    ```json
    // tsconfig.app.json ::
    
    /*Paths for ShadcnUI*/
        "baseUrl": ".",
        "paths": {
          "@/*": [
            "./@/*"
          ]
        }
      },
      "include": ["src", "@"]
    ```
    ---
    ```typescript
    // vite.config.ts ::
    
    import path from "path"
    import { defineConfig } from 'vite'
    import react from '@vitejs/plugin-react'
    
    // https://vitejs.dev/config/
    
    export default defineConfig({
      plugins: [react()],
      resolve: {
        alias: {
          "@": path.resolve(__dirname, "./@"),
        },
      },
    })
    ```
    
    - Step 3 :
    - Install components
    ```bash
    npx shadcn-ui@latest add [component]
    ```
    ```bash
    Which components would you like to add? › Space to select. A to toggle all.Enter to submit.
    ◯ accordion
    ◯ alert
    ◯ alert-dialog
    ◯ aspect-ratio
    ◯ avatar
    ◯ badge
    ◯ button
    ◯ calendar
    ◯ card
    ◯ checkbox
    ```
    
    - Step 4 :
    ```typescript
    import { useState } from 'react';
    import { Button } from "@/components/ui/button"
    
    import { Person } from './components/Person.tsx';
    
    function App() {
      const [value, setValue] = useState<boolean>(true);
      
      const toggleInfo = () => {
        setValue((prev) => !prev)
      }
    
      return (
        <>
          <div className=''>
            <Person value={value} />
          </div>
          <Button onClick={toggleInfo}>Toggle value</Button>
        </>
      )
    }
    
    export default App
    ```

</details>



<details>
<summary>Animation in CSS</summary>
<br>
  
> ### **`Animation in CSS`** :
- animation-fill-mode:
  - The animation-fill-mode property determines the styles applied to an element before and after the animation.
  - It can take the following values:
      - none: The default value. The element will not retain any styles from the animation before or after it runs.
      - forwards: The element will retain the styles of the last keyframe after the animation completes. This is useful if you want the final state of the animation to persist.
      - backwards: The element will apply the styles of the first keyframe before the animation starts. This can be useful if you want the initial state of the animation to be applied even before the animation begins.
      - both: Equivalent to setting both forwards and backwards. The element will retain styles from the first keyframe before the animation starts and from the last keyframe after it completes.

- animation-direction:
  - The animation-direction property determines the direction of the animation sequence, whether it proceeds forward, backward, or alternates between forward and backward.
  - It can take the following values:
      - normal: The animation runs forward from the beginning to the end.
      - reverse: The animation runs backward from the end to the beginning.
      - alternate: The animation alternates between running forward and backward. If the iteration count is even, it runs forward, and if it's odd, it runs backward.
      - alternate-reverse: Similar to alternate, but it starts by running backward.
<br>
[Motion Graphic Design & Animation Principles Website - Zajno Digital Studio](https://motion.zajno.com/)
[Locomotive Scroll](https://locomotivemtl.github.io/locomotive-scroll/)
</details>


<details>
<summary>Harkirat Roadmap for Full-Stack Development</summary>
<br>

> ### **`Harkirat Roadmap for Full-Stack Development`** :
### Basics ⇒
  - Foundation
    - Foundation Javascript, async nature of JS 
    - Node.js and its runtime
    - Databases (NoSQL/SQL)
    - Mongo and Postgres deep dive
    - Typescript beginner to advance

  - Backend
    - Backend communication protocols
    - Express basic to advance
    - ORMS
    - Middlewares, routes, status codes, global catches
    - Zod
    - Husky
    - MonoRepos, turborepo
    - Serverless Backends
    - OpenAPI Spec
    - Autogenerated clients
    - Authentication using external libraries
    - Scaling Node.js, performance benchmarks 
    - Deploying npm packages

  - Frontend
    - Reconcilers and Frontend frameworks
    - React beginner to advance
    - Internals of state, Context API
    - State management using recoil
    - CSS you need to know of, Flexbox, basic styling
    - Frontend UI frameworks, Deep dive into Tailwind 
    - Containerization, Docker
    - Next.js
    - Custom hooks
    - In house auth using next auth

  - Basic Devops
    - Docker end to end 
    - Deploying to AWS servers 
    - Newer clouds like fly/Remix 
    - Nginx and reverse proxies

  - Projects
    - GSOC Project setting up and issue solving 
    - Building Paytm/Wallet End to End

### Advance ⇒
  - Advanced Backend, System Design
    - Advanced backend communication
    - Message queues and PubSubs
    - Proxies, Load balancers
    - Redis Deep dive
    - Kafka Deep dive
    - Common Design Patterns in JS
    - Advanced DB concepts (Indexing, normalization)
    - Rate limiting
    - Captchas and DDoS protection
    - Sharding, Replication, Resiliency
    - Horizontal and vertical scaling
    - Polling and websockets
    - Grpc
    - Capacity Estimation Load Balancers
    - CAP Theorem
    - Testing Node.js Apps in 2023
    - Real time communication, basics of WebRTC

  - Advanced DevOps
    - Docker Deep dive
    - Container orchestration, Docker Swarm 
    - Kubernetes
    - CI/CD
    - Monitoring systems basics to advance 
    - Promhetheus, Grafana
    - Newrelic as a paid service
    - Serverless Deep dive
    - AWS Constructs (EC2, S3, CDNs, LB, EKS)

  - Projects
    - Zerodha end to end
    - Zapier end to end
    - Real world open source projects



</details>
<details>
<summary>tools/websites</summary>
<br>

- [Free for Developers (free-for.dev)](https://free-for.dev/#/)
- [Motion Graphic Design & Animation Principles Website - Zajno Digital Studio](https://motion.zajno.com/)
- [list of new tools to use in websites](https://www.pillarstack.com/)
- [No-code Animations](https://www.typefaceanimator.com/)
- [WEB Free Fonts for Windows and Mac / Font free Download - OnlineWebFonts.COM](https://www.onlinewebfonts.com/fonts)
- [Free Font Downloads](https://www.freefaces.gallery/)
- [Animated logos & stickers](https://www.lottielab.com/)
- [Dribbble](https://dribbble.com/shots)
- [CHEATSHEATS](https://overapi.com/)
- [CHEATSHEATS](https://quickref.me/)
- [Logo Maker](https://www.shopify.com/tools/logo-maker)
- [Illustrations](http://storyset.com)
- [Illustrations](https://sapiens.ui8.net/6f3c3c2)
- [Illustrations and assests](https://ultima.storytale.io/)
- [3D Illustrations](http://pixcap.com)
- [FFFuel](https://fffuel.co/)
- [PatternPad - Create beautiful patterns for presentations, social media or branding.](https://patternpad.com/)
- [Simple Backgrounds](https://bgjar.com/)
- [Create images of your code](https://ray.so/)
- [Color Palettes](https://coolors.co/)
- [Color Palettes](https://palettemaker.com/)
- [Icons SVG](https://icones.js.org/)
- [Icons](https://iconer.app/)
- [To create shadows Neumorphism](https://neumorphism.io/#e0e0e0)
- [Free Assests](https://www.waveindex.com/collections/freebies)
- [Free Images](https://unsplash.com/)
- [Free Texture](https://texturelabs.org/)
- [Archive Images](https://picryl.com/)
- [Free Mockups](https://www.mockupworld.co/)
- [Design Inspo](https://savee.it/)
- [HTML Templates](https://htmlrev.com/)
- [CSS jokes](https://comicss.art/)

</details>
<details>
<summary>Articles</summary>
<br>

- [51 CSS Animations on Scroll Your Visitors Will Love (sliderrevolution.com)](https://www.sliderrevolution.com/resources/css-animations-on-scroll/)
- [How To Use Preload and Prefetch in HTML to Load Assets](https://www.digitalocean.com/community/tutorials/html-preload-prefetch)
- [useLayoutEffect and useEffect.](https://www.instagram.com/p/C2kaG8HgKPH/)
- Worker script and generator function in JavaScript.
- Suspense in react

### Deployment of vite + react app : 
  - [Deploying Vite App to GitHub Pages - DEV Community](https://dev.to/shashannkbawa/deploying-vite-app-to-github-pages-3ane)
  - [React to Vercel: Deployment Made Easy. - DEV Community](https://dev.to/codeparrot/react-to-vercel-deployment-made-easy-bg2)
  - [Changing the input and output directory in Vite - Stack Overflow](https://stackoverflow.com/questions/66863200/changing-the-input-and-output-directory-in-vite#:~:text=You%20can%20set%20up%20your%20vite.config.js%20like%20this%3A,root%3A%20path.resolve%28__dirname%2C%20%27src%27%29%2C%20build%3A%20%7B%20outDir%3A%20path.resolve%28__dirname%2C%20%27dist%27%29%2C)


</details>

<details>
<summary>For Ideas</summary>
<br>
  
- [tympanus](https://tympanus.net/codrops/)
- [No-code Animations](https://www.typefaceanimator.com/)

</details>
