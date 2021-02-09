- Electron: Building Cross Platform Desktop Apps
    - 1 hr 54 min
    - Intermediate
    - Released: 05/28/2019
    - Ray Villalobos
    - Linked-In Learning:
    - [URL](https://www.linkedin.com/learning/electron-building-cross-platform-desktop-apps-3/cross-platform-apps-with-electron)
    - [Repository](https://github.com/planetoftheweb/electron-4)

- Installing Electron:
    - Latest stable version as of recording: 4.1.4
        ```javascript
            npm init -y
            npm install --save-dev electron@4.1.4
            {
                "main": "index.js",
                "scripts": {
                    "start": "electron ."
                }
            }
        ```
    - index.js

- Exploring Electron Features:
    - Configuration: Designed to work with Windows, Macintoash, and perhaps Linux.
    - Inter-process Communication:
        - Process 1: IPC Main. Handling aplication.
        - Process 2: IPC Renderer. Handling the rendering.

        - Execute some node-type of execution:
        ```javascript
            webPreferences: {
                nodeIntegration: true
            },
        ```
        - So that we can perform the following:
        ```html
            <script>
                const { ipcRenderer } = require('electron');
            </script>
        ```

        ```javascript
            const { app, BrowserWindow, ipcMain } = require('electron');
            const URL = 'https://7ty.tech';

            app.on('ready', () => {
                let window = new BrowserWindow({
                    width: 600,
                    height: 800,
                    center: true,
                    minWidth: 300,
                    movable: true,
                    minimizable: false,
                    show: false
                });
                window.loadURL(URL);

                let about = new BrowserWindow({
                    width: 300,
                    height: 300,
                    frame: false,
                    webPreferences: {
                        nodeIntegration: true
                    },
                    show: false
                });
                about.loadFile('./about.html');

                window.on('closed', () => {
                    appWindow = null;
                });

                window.once('ready-to-show', () => {
                    window.maximize();
                    window.show();
                    setTimeout(() => {
                        about.show();
                        // setTimeout(() => {
                        //     about.hide();
                        // }, 3000);
                    }, 1000);
                });

                ipcMain.on('close', event => {
                    about.hide();
                })
            });
        ```

        ```html
            <html>
                <head></head>
                <body>
                    <hr />
                    <h4>
                        About
                    </h4>
                    <p>
                        Born in fields of snow, James soon grew taller.
                    </p>
                    <a href="#" id="close">Close</a>
                    <script>
                        const { ipcRenderer } = require('electron');
                        document.querySelector('#close').addEventListener('click', () => {
                            ipcRenderer.send('close');
                        });
                    </script>
                </body>
            </html>
        ```

- Using Vue.js:
    - Could also use React. e.g.: Applications that work with interfaces.
    - Add router. (Without history.)
    ```javascript
        npm install -g @vue/cli
        vue add electron-builder
    ```
    - So now what?
    - Addition of a background.js file with addition "run" commands.
    ```javascript
        npm run electron:serve
    ```
    - [Hacked Code](https://github.com/planetoftheweb/vue-essentials)
    - You get: Vue Web within an Electron wrapper.
    ```javascript
        npm i @fortawesome/fontawesome-free
        npm i @fortawesome/fontawesome-svg-core
        npm i @fortawesome/free-solid-svg-icons
        npm i @fortawesome/vue-fontawesome
        npm i animate.css
        npm i bootstrap
        npm i jquery
        npm i popper.js
    ```
    - Snippet *before* my forced/hacked updates:
    ```html
        <template>
        <transition-group name="fade" tag="div" @beforeEnter="beforeEnter" @enter="enter" @leave="leave">
            <div
            class="row d-flex mb-3 align-items-center"
            v-for="(item, index) in products"
            :key="item.id"
            v-if="item.price<=Number(maximum)"
            :data-index="index"
            >
    ```

    ```html
        <script>
        import Price from "./Price.vue";
        import VueRouter from "vue-router";

        props: ["cart", "cartQty", "cartTotal"],
        components: {
            FontAwesomeIcon,
            VueRouter,
            Price
        }
    ```
