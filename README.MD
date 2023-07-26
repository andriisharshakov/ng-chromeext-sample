# Install the extension

Open your Chrome browser and navigate to chrome://extensions.

Enable Developer Mode by clicking the toggle switch next to Developer mode. Click the “Load unpacked” button and select the extension directory of our repo containing ourmanifest.json.

# Set up Angular application

Now, let’s set up our Angular application in a subfolder of our repository.

We can do this by running:

```
npx -p @angular/cli ng new angular-chrome-app
```

or just (if you have installed the Angular CLI):

```
ng new angular-chrome-app
```