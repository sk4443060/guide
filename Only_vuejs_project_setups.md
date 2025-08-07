FOLLOW VUE JS OFFICIAL DOCS: https://vuejs.org/guide/quick-start.html

[01] Copy, paste and hit enter into your terminal
     @ npm create vue@latest
     
[02] Select options as per your need
     ✔ Project name: … <your-project-name>
     ✔ Add TypeScript? … No / Yes
     ✔ Add JSX Support? … No / Yes
     ✔ Add Vue Router for Single Page Application development? … No / Yes
     ✔ Add Pinia for state management? … No / Yes
     ✔ Add Vitest for Unit testing? … No / Yes
     ✔ Add an End-to-End Testing Solution? … No / Cypress / Nightwatch / Playwright
     ✔ Add ESLint for code quality? … No / Yes
     ✔ Add Prettier for code formatting? … No / Yes
     ✔ Add Vue DevTools 7 extension for debugging? (experimental) … No / Yes

     Scaffolding project in ./<your-project-name>...
     Done.

[03] Make sure the initial folder structure as
WEBSITE
|- .vscode/
|- node_modules/
|- public
|- src
   |- assets/
   |- components/
       |- Navbar.vue
       |- Footer.vue
   |- layouts/
       |- DefaultLayout.vue (Yeh layout har page (like Home, About, etc.) ke around Navbar aur Footer ko wrap karega.)
   |- router/
       |- index.js
   |- store/
   |- utils/
   |- views/
       |- Home.vue  (This is the layout for the home page)
   |- App.vue
   |- main.js
|- package.json
   |- package-lock.json
|- README.md
|- vite.config.js

[04] COMPONENT CODE BLOCK (There are three types of code blocks as):

      [BLOCK_01] HTML SCELETON GOES INSIDE TEMPLATE
      <template>
          <nav class="navbar">
          <div class="logo">MySite</div>
          <ul class="nav-links">
            <li><router-link to="/">Home</router-link></li>
            <li><router-link to="/about">About</router-link></li>
            <li><router-link to="/contact">Contact</router-link></li>
          </ul>
        </nav>
      </template>
      
      [BLOCK_02] SCRIPT CODE GOES INSIDE SCRIPT BLOCK
      <script>
        export default {
          name: 'Navbar',
        }
      </script>

      [BLOCK_03] CORRESPONDING STYLE GOES INSIDE STYLE BLOCK AS
      <style scoped>
        .navbar {
          display: flex;
          justify-content: space-between;
          padding: 1rem 2rem;
          background-color: #222;
          color: white;
        }
        .nav-links {
          list-style: none;
          display: flex;
          gap: 1rem;
        }
        a {
          color: white;
          text-decoration: none;
        }
        </style>

[05] LAYOUT SKELETON AS (SAME AS COMPONENT SKELETON) STYLE IS OPTIONAL BCZ COMPONENTS BRINGS ITS ON CSS

      <template>
        <div>
          <Navbar />
          <main>
            <slot />
          </main>
          <Footer />
        </div>
      </template>

    <script>
      import Navbar from '../components/Navbar.vue'
      import Footer from '../components/Footer.vue'
      
      export default {
        name: 'DefaultLayout',
        components: {
          Navbar,
          Footer
        }
      }
    </script>

[06] SETUP ROUTER FOLLOW AS: (router > index.js)

    // src/router/index.js
    import { createRouter, createWebHistory } from 'vue-router'
    import Home from '../views/Home.vue'
    
    const routes = [
      {
        path: '/',
        name: 'Home',
        component: Home,
      },
    ]
    
    const router = createRouter({
      history: createWebHistory(),
      routes,
    })
    
    export default router

[07] SETUP VIEWS FILE (views > Home.vue)

    <template>
      <div class="home-page">
        <h1>Welcome to MySite!</h1>
        <p>This is the home page.</p>
      </div>
    </template>
  
    <script>
      export default {
        name: 'Home',
      }
    </script>
