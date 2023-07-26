# Creating your own Chrome Extensions is easier than many may think. And it’s a lot of fun. We can let our creativity run wild and modify each website as we want it to.

[Source](https://web-highlights.com/blog/how-to-build-a-chrome-extension-using-angular)

In this article, I will show you how to set up a Chrome Extension in general. Afterward, we will set up an Angular application and load it on any website.

### Setup

Before we start, let’s create two subfolders in our repository: **_extension_** and **_angular-chrome-app_**. The **_extension_** folder will contain our chrome extension files, and we will create an Angular app in the **_angular-chrome-app_** directory.

The structure should look like this:

![Repository folder structure](https://cdn-images-1.medium.com/max/1760/1*92hkdAK2ne8AnXmWEFv2gg.png)

Repository folder structure

### Chrome Extension Setup

Let’s dive right into the setup of our Chrome extension. First of all, we need to create a `manifest.json` file. We will create the file in our **_extension_** subfolder.

The manifest is the entry point of our extension, which defines metadata, such as name and version, as well as additional functionalities.

#### Create manifest.json

Let’s create a `manifest.json` and add some metadata:

The first three values `name` , `version` and `manifest_version` are sufficient to create our first chrome extension.

#### Install the extension

Open your Chrome browser and navigate to **chrome://extensions**.

Enable Developer Mode by clicking the toggle switch next to **Developer mode**. Click the “**Load unpacked”** button and select the **_extension_** directory of our repo containing our`manifest.json`.

![Screenshot: How to load unpacked Chrome extension](https://cdn-images-1.medium.com/max/1760/1*W5rm8itxo70rfLrdtd3VKQ.png)

Load unpacked Chrome extension

Congratulations! You’ve just created a Chrome Extension!

### Set up Angular application

Now, let’s set up our Angular application in a subfolder of our repository.

We can do this by running:

`npx -p @angular/cli ng new angular-chrome-app`

or just (if you have installed the Angular CLI):

`ng new angular-chrome-app`

Now, let’s eliminate all the unnecessary stuff in the `app.component.html` file. For this article, let’s put a simple _“Hello from Angular App”_ headline to our component:

<table data-hpc="" data-tab-size="8" data-paste-markdown-skip="" data-tagsearch-lang="TypeScript" data-tagsearch-path="app.component.ts"><tbody><tr><td id="file-app-component-ts-L1" data-line-number="1"></td><td id="file-app-component-ts-LC1"><span>import</span> <span>{</span> <span>Component</span> <span>}</span> <span>from</span> <span>'@angular/core'</span><span>;</span></td></tr><tr><td id="file-app-component-ts-L2" data-line-number="2"></td><td id="file-app-component-ts-LC2"></td></tr><tr><td id="file-app-component-ts-L3" data-line-number="3"></td><td id="file-app-component-ts-LC3">@<span>Component</span><span>(</span><span>{</span></td></tr><tr><td id="file-app-component-ts-L4" data-line-number="4"></td><td id="file-app-component-ts-LC4"><span>selector</span>: <span>'app-root'</span><span>,</span></td></tr><tr><td id="file-app-component-ts-L5" data-line-number="5"></td><td id="file-app-component-ts-LC5"><span>templateUrl</span>: <span>'./app.component.html'</span><span>,</span></td></tr><tr><td id="file-app-component-ts-L6" data-line-number="6"></td><td id="file-app-component-ts-LC6"><span>styleUrls</span>: <span>[</span><span>'./app.component.scss'</span><span>]</span><span>,</span></td></tr><tr><td id="file-app-component-ts-L7" data-line-number="7"></td><td id="file-app-component-ts-LC7"><span>}</span><span>)</span></td></tr><tr><td id="file-app-component-ts-L8" data-line-number="8"></td><td id="file-app-component-ts-LC8"><span>export</span> <span>class</span> <span>AppComponent</span> <span>{</span></td></tr><tr><td id="file-app-component-ts-L9" data-line-number="9"></td><td id="file-app-component-ts-LC9"><span>title</span> <span>=</span> <span>'Angular App'</span><span>;</span></td></tr><tr><td id="file-app-component-ts-L10" data-line-number="10"></td><td id="file-app-component-ts-LC10"><span>}</span></td></tr></tbody></table>

As we want to include the Angular app in our Chrome Extension, we need to configure how Angular sets up our application. For that, we need to change the `main.ts` file:

<table data-hpc="" data-tab-size="8" data-paste-markdown-skip="" data-tagsearch-lang="TypeScript" data-tagsearch-path="main.ts"><tbody><tr><td id="file-main-ts-L1" data-line-number="1"></td><td id="file-main-ts-LC1"><span>import</span> <span>{</span> <span>platformBrowserDynamic</span> <span>}</span> <span>from</span> <span>'@angular/platform-browser-dynamic'</span><span>;</span></td></tr><tr><td id="file-main-ts-L2" data-line-number="2"></td><td id="file-main-ts-LC2"></td></tr><tr><td id="file-main-ts-L3" data-line-number="3"></td><td id="file-main-ts-LC3"><span>import</span> <span>{</span> <span>AppModule</span> <span>}</span> <span>from</span> <span>'./app/app.module'</span><span>;</span></td></tr><tr><td id="file-main-ts-L4" data-line-number="4"></td><td id="file-main-ts-LC4"></td></tr><tr><td id="file-main-ts-L5" data-line-number="5"></td><td id="file-main-ts-LC5"><span>const</span> <span>ROOT_ELEMENT_TAG</span> <span>=</span> <span>'app-root'</span><span>;</span></td></tr><tr><td id="file-main-ts-L6" data-line-number="6"></td><td id="file-main-ts-LC6"></td></tr><tr><td id="file-main-ts-L7" data-line-number="7"></td><td id="file-main-ts-LC7"><span>let</span> <span>rootElement</span> <span>=</span> <span>document</span><span>.</span><span>querySelector</span><span>(</span><span>ROOT_ELEMENT_TAG</span><span>)</span><span>;</span></td></tr><tr><td id="file-main-ts-L8" data-line-number="8"></td><td id="file-main-ts-LC8"></td></tr><tr><td id="file-main-ts-L9" data-line-number="9"></td><td id="file-main-ts-LC9"><span>if</span> <span>(</span><span>!</span><span>rootElement</span><span>)</span> <span>{</span></td></tr><tr><td id="file-main-ts-L10" data-line-number="10"></td><td id="file-main-ts-LC10"><span>rootElement</span> <span>=</span> <span>document</span><span>.</span><span>createElement</span><span>(</span><span>ROOT_ELEMENT_TAG</span><span>)</span><span>;</span></td></tr><tr><td id="file-main-ts-L11" data-line-number="11"></td><td id="file-main-ts-LC11"><span>rootElement</span><span>.</span><span>id</span> <span>=</span> <span>'angular-chrome-app'</span><span>;</span></td></tr><tr><td id="file-main-ts-L12" data-line-number="12"></td><td id="file-main-ts-LC12"><span>document</span><span>.</span><span>body</span><span>.</span><span>appendChild</span><span>(</span><span>document</span><span>.</span><span>createElement</span><span>(</span><span>ROOT_ELEMENT_TAG</span><span>)</span><span>)</span><span>;</span></td></tr><tr><td id="file-main-ts-L13" data-line-number="13"></td><td id="file-main-ts-LC13"><span>}</span></td></tr><tr><td id="file-main-ts-L14" data-line-number="14"></td><td id="file-main-ts-LC14"></td></tr><tr><td id="file-main-ts-L15" data-line-number="15"></td><td id="file-main-ts-LC15"><span>platformBrowserDynamic</span><span>(</span><span>)</span></td></tr><tr><td id="file-main-ts-L16" data-line-number="16"></td><td id="file-main-ts-LC16"><span>.</span><span>bootstrapModule</span><span>(</span><span>AppModule</span><span>)</span></td></tr><tr><td id="file-main-ts-L17" data-line-number="17"></td><td id="file-main-ts-LC17"><span>.</span><span>catch</span><span>(</span><span>(</span><span>err</span><span>)</span> <span>=&gt;</span> <span>console</span><span>.</span><span>error</span><span>(</span><span>err</span><span>)</span><span>)</span><span>;</span></td></tr></tbody></table>

To use our app on any website, we can not assume anymore that the `<app-root>` element exists that is usually provided by our `index.html` file. That’s why we will create our own root element programmatically before rendering the application.

We check whether there is an existing `<app-root>` element in the DOM. If not, we will create a new one and append it to the document body.

Finally, let’s create some global styles within the `styles.scss` file to position our App visibly on the left side of the screen:

<table data-hpc="" data-tab-size="8" data-paste-markdown-skip="" data-tagsearch-lang="SCSS" data-tagsearch-path="styles.scss"><tbody><tr><td id="file-styles-scss-L1" data-line-number="1"></td><td id="file-styles-scss-LC1"><span>app-root</span> {</td></tr><tr><td id="file-styles-scss-L2" data-line-number="2"></td><td id="file-styles-scss-LC2"><span><span>position</span></span>: <span>fixed</span>;</td></tr><tr><td id="file-styles-scss-L3" data-line-number="3"></td><td id="file-styles-scss-LC3"><span><span>left</span></span>: <span>0</span>;</td></tr><tr><td id="file-styles-scss-L4" data-line-number="4"></td><td id="file-styles-scss-LC4"><span><span>top</span></span>: <span>0</span>;</td></tr><tr><td id="file-styles-scss-L5" data-line-number="5"></td><td id="file-styles-scss-LC5"><span><span>width</span></span>: <span>300<span>px</span></span>;</td></tr><tr><td id="file-styles-scss-L6" data-line-number="6"></td><td id="file-styles-scss-LC6"><span><span>height</span></span>: <span>100<span>vh</span></span>;</td></tr><tr><td id="file-styles-scss-L7" data-line-number="7"></td><td id="file-styles-scss-LC7"><span><span>background</span></span>: <span>#ffffff</span>;</td></tr><tr><td id="file-styles-scss-L8" data-line-number="8"></td><td id="file-styles-scss-LC8"><span><span>border-right</span></span>: <span>1<span>px</span></span> <span>solid</span> <span>#c2c2c2</span>;</td></tr><tr><td id="file-styles-scss-L9" data-line-number="9"></td><td id="file-styles-scss-LC9"><span><span>z-index</span></span>: <span>999</span>;</td></tr><tr><td id="file-styles-scss-L10" data-line-number="10"></td><td id="file-styles-scss-LC10">}</td></tr></tbody></table>

### Include Angular App into Chrome Extension

In the beginning, we already installed our extension. Still, currently, it doesn’t do anything because we haven’t added functionality to our `manifest.json` .

#### Create a Content Script

To include our Angular App in any webpage, we need a way to read the DOM and make changes to it.

For that, we will create a content script:

> **_Content scripts_** _live in an isolated world, allowing a content script to make changes to its JavaScript environment without conflicting with the page or other extensions’ content Scripts. —_ [developer.chrome.com](https://developer.chrome.com/docs/extensions/mv2/content_scripts/)

For starters, let’s create a `content.js` file with an alert to ensure that our extension successfully loads the script. This file will act as our content script.

The `content.js` script is the entry point of our extension. Let’s adjust our `manifest.json` to inject our script:

<table data-hpc="" data-tab-size="8" data-paste-markdown-skip="" data-tagsearch-lang="JSON" data-tagsearch-path="manifest.json"><tbody><tr><td id="file-manifest-json-L1" data-line-number="1"></td><td id="file-manifest-json-LC1">{</td></tr><tr><td id="file-manifest-json-L2" data-line-number="2"></td><td id="file-manifest-json-LC2"><span>"name"</span>: <span><span>"</span>Angular Chrome Extension<span>"</span></span>,</td></tr><tr><td id="file-manifest-json-L3" data-line-number="3"></td><td id="file-manifest-json-LC3"><span>"version"</span>: <span><span>"</span>1.0.0<span>"</span></span>,</td></tr><tr><td id="file-manifest-json-L4" data-line-number="4"></td><td id="file-manifest-json-LC4"><span>"manifest_version"</span>: <span>3</span>,</td></tr><tr><td id="file-manifest-json-L5" data-line-number="5"></td><td id="file-manifest-json-LC5"><span>"content_scripts"</span>: [</td></tr><tr><td id="file-manifest-json-L6" data-line-number="6"></td><td id="file-manifest-json-LC6">{</td></tr><tr><td id="file-manifest-json-L7" data-line-number="7"></td><td id="file-manifest-json-LC7"><span>"matches"</span>: [<span><span>"</span>&lt;all_urls&gt;<span>"</span></span>],</td></tr><tr><td id="file-manifest-json-L8" data-line-number="8"></td><td id="file-manifest-json-LC8"><span>"js"</span>: [</td></tr><tr><td id="file-manifest-json-L9" data-line-number="9"></td><td id="file-manifest-json-LC9"><span><span>"</span>content.js<span>"</span></span></td></tr><tr><td id="file-manifest-json-L10" data-line-number="10"></td><td id="file-manifest-json-LC10">]</td></tr><tr><td id="file-manifest-json-L11" data-line-number="11"></td><td id="file-manifest-json-LC11">}</td></tr><tr><td id="file-manifest-json-L12" data-line-number="12"></td><td id="file-manifest-json-LC12">]</td></tr><tr><td id="file-manifest-json-L13" data-line-number="13"></td><td id="file-manifest-json-LC13">}</td></tr></tbody></table>

To use our statically declared `content.js` script we need to register it under the `content_scripts` field. This field needs to define the _required_ attribute `matches` to specify on which pages the content script will be injected. For that, you can set several [match patterns](https://developer.chrome.com/docs/extensions/mv3/content_scripts/match_patterns). We will use the special pattern `<all_urls>` to match any URL that starts with a permitted scheme- for example `http` or `https` .

We also define the optional field `js`. Here we define our scripts to be injected into matching pages.

Let’s update our extension by pressing the refresh button of the extension on `chrome://extensions` . We can now navigate to any page, and if done correctly, an alert should appear when the page is loaded.

![Screenshot showing alert on Medium.com](https://cdn-images-1.medium.com/max/1760/1*L--jyGGyNT7tWGSDOIMl0A.png)

Worst Chrome Extension ever, right? Let’s continue and include Angular.

#### Create an Angular Content Script

Let’s build our Angular application by running `yarn build` or `npm run build`.

You should see that the react-scripts build script generates some Javascript files in the **_/dist/angular-chrome-app_** folder:

![Screenshot: Angular build folder](https://cdn-images-1.medium.com/max/1760/1*dqETET9_8S-ii2mCpn-pMA.png)

Angular build folder

From the generated `index.html` we can derive which files are necessary to make the application work:

<table data-hpc="" data-tab-size="8" data-paste-markdown-skip="" data-tagsearch-lang="HTML" data-tagsearch-path="index.html"><tbody><tr><td id="file-index-html-L1" data-line-number="1"></td><td id="file-index-html-LC1"><span>&lt;</span><span>body</span><span>&gt;</span></td></tr><tr><td id="file-index-html-L2" data-line-number="2"></td><td id="file-index-html-LC2"><span>&lt;</span><span>app-root</span><span>&gt;</span><span>&lt;/</span><span>app-root</span><span>&gt;</span></td></tr><tr><td id="file-index-html-L3" data-line-number="3"></td><td id="file-index-html-LC3"><span>&lt;</span><span>script</span> <span>src</span>="<span>runtime.b46334b3af268ec4.js</span>" <span>type</span>="<span>module</span>"<span>&gt;</span><span>&lt;/</span><span>script</span><span>&gt;</span></td></tr><tr><td id="file-index-html-L4" data-line-number="4"></td><td id="file-index-html-LC4"><span>&lt;</span><span>script</span> <span>src</span>="<span>polyfills.8d28de284ef0dd8f.js</span>" <span>type</span>="<span>module</span>"<span>&gt;</span><span>&lt;/</span><span>script</span><span>&gt;</span></td></tr><tr><td id="file-index-html-L5" data-line-number="5"></td><td id="file-index-html-LC5"><span>&lt;</span><span>script</span> <span>src</span>="<span>main.87d969ee394c36a6.js</span>" <span>type</span>="<span>module</span>"<span>&gt;</span><span>&lt;/</span><span>script</span><span>&gt;</span></td></tr><tr><td id="file-index-html-L6" data-line-number="6"></td><td id="file-index-html-LC6"><span>&lt;/</span><span>body</span><span>&gt;</span></td></tr></tbody></table>

We can see that three JavaScript files are loaded to make our Angular application work:

-   **runtime**.\[hash\].js
-   **polyfills**.\[hash\].js
-   **main**.\[hash\].js

What we now want to do is not load the main file from the `index.html` but within our Chrome extension as a content script.

#### Copy build files to the extension

We could now go ahead and copy & paste all of the three files mentioned above and include them in our `manifest.json`.

But, as the hashes in the filename change after each build, we should automate this. Notice that we could set up Webpack here but let’s keep things simple and just copy all files needed and adjust their filename after each build.

To do that, we create a new script in our `package.json` which will execute those three commands

This will copy all necessary files into our **_/extension_** folder and removes the hashes from the file names. Also, notice that we include our global styles.

Here are our updated scripts in the `package.json` in the **_/angular-chrome-app_** folder:

<table data-hpc="" data-tab-size="8" data-paste-markdown-skip="" data-tagsearch-lang="JSON" data-tagsearch-path="package.json"><tbody><tr><td id="file-package-json-L1" data-line-number="1"></td><td id="file-package-json-LC1"><span>"scripts"</span>: {</td></tr><tr><td id="file-package-json-L2" data-line-number="2"></td><td id="file-package-json-LC2"><span>"ng"</span>: <span><span>"</span>ng<span>"</span></span>,</td></tr><tr><td id="file-package-json-L3" data-line-number="3"></td><td id="file-package-json-LC3"><span>"start"</span>: <span><span>"</span>ng serve<span>"</span></span>,</td></tr><tr><td id="file-package-json-L4" data-line-number="4"></td><td id="file-package-json-LC4"><span>"build"</span>: <span><span>"</span>ng build &amp;&amp; yarn copy:build<span>"</span></span>,</td></tr><tr><td id="file-package-json-L5" data-line-number="5"></td><td id="file-package-json-LC5"><span>"copy:build"</span>: <span><span>"</span>cp dist/angular-chrome-app/main*.js ../extension/main.js &amp; cp dist/angular-chrome-app/polyfills*.js ../extension/polyfills.js &amp; cp dist/angular-chrome-app/runtime*.js ../extension/runtime.js &amp; cp dist/angular-chrome-app/styles*.css ../extension/styles.css<span>"</span></span>,</td></tr><tr><td id="file-package-json-L6" data-line-number="6"></td><td id="file-package-json-LC6"><span>"watch"</span>: <span><span>"</span>ng build --watch --configuration development<span>"</span></span>,</td></tr><tr><td id="file-package-json-L7" data-line-number="7"></td><td id="file-package-json-LC7"><span>"test"</span>: <span><span>"</span>ng test<span>"</span></span></td></tr><tr><td id="file-package-json-L8" data-line-number="8"></td><td id="file-package-json-LC8">},</td></tr></tbody></table>

After each build, we copy the build files to our **_/extension_** folder in which we can now include them by adding them as content scripts like this:

<table data-hpc="" data-tab-size="8" data-paste-markdown-skip="" data-tagsearch-lang="JSON" data-tagsearch-path="manifest.json"><tbody><tr><td id="file-manifest-json-L1" data-line-number="1"></td><td id="file-manifest-json-LC1">{</td></tr><tr><td id="file-manifest-json-L2" data-line-number="2"></td><td id="file-manifest-json-LC2"><span>"name"</span>: <span><span>"</span>Angular Chrome Extension<span>"</span></span>,</td></tr><tr><td id="file-manifest-json-L3" data-line-number="3"></td><td id="file-manifest-json-LC3"><span>"version"</span>: <span><span>"</span>1.0.0<span>"</span></span>,</td></tr><tr><td id="file-manifest-json-L4" data-line-number="4"></td><td id="file-manifest-json-LC4"><span>"manifest_version"</span>: <span>3</span>,</td></tr><tr><td id="file-manifest-json-L5" data-line-number="5"></td><td id="file-manifest-json-LC5"><span>"content_scripts"</span>: [</td></tr><tr><td id="file-manifest-json-L6" data-line-number="6"></td><td id="file-manifest-json-LC6">{</td></tr><tr><td id="file-manifest-json-L7" data-line-number="7"></td><td id="file-manifest-json-LC7"><span>"matches"</span>: [<span><span>"</span>&lt;all_urls&gt;<span>"</span></span>],</td></tr><tr><td id="file-manifest-json-L8" data-line-number="8"></td><td id="file-manifest-json-LC8"><span>"js"</span>: [<span><span>"</span>runtime.js<span>"</span></span>, <span><span>"</span>polyfills.js<span>"</span></span>, <span><span>"</span>main.js<span>"</span></span>],</td></tr><tr><td id="file-manifest-json-L9" data-line-number="9"></td><td id="file-manifest-json-LC9"><span>"css"</span>: [<span><span>"</span>styles.css<span>"</span></span>]</td></tr><tr><td id="file-manifest-json-L10" data-line-number="10"></td><td id="file-manifest-json-LC10">}</td></tr><tr><td id="file-manifest-json-L11" data-line-number="11"></td><td id="file-manifest-json-LC11">]</td></tr><tr><td id="file-manifest-json-L12" data-line-number="12"></td><td id="file-manifest-json-LC12">}</td></tr></tbody></table>

Now, we can go ahead and re-load the extension to apply our changes.

![Screenshot: How to reload extension by clicking reload icon](https://cdn-images-1.medium.com/max/1760/1*wnreH0oI6mC3wbb0zlVGQg.png)

When navigating to any webpage, we should see our Angular application showing up on the left side of the screen:

![Screenshot: Angular App loaded in Chrome Extension](https://cdn-images-1.medium.com/max/1760/1*XtA01UaJ3U2pswjpCYwfBw.png)

Angular App loaded in Chrome Extension

Admittedly, this is still not a cool Chrome Extension. But now that we’ve successfully integrated our Angular app into a Chrome extension, you can build any app of your choice with Angular that runs on any webpage.

You can find the code of this article in this [GitHub repository](https://github.com/MariusBongarts/react-chrome-extension).

### Final Thoughts

Creating your own Chrome Extension is much easier than many may think. Once you set up the extension correctly, you can develop whatever you want using Angular. Being able to design your very own Chrome extension can be a lot of fun as you can let your creativity run wild.

I am always happy to answer questions and am open to criticism. Get in touch with me via [**LinkedIn**](https://www.linkedin.com/in/marius-bongarts-6b3638171/) or [**Twitter**](https://twitter.com/MariusBongarts)**.**