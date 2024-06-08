# Teamplate iFrame Widget

This teamplate is mean to be used to create new experiences that can be included using iFrames into other application and websites.

## Installation

Create a new repository from this template.

Clone your new repository to your local machine.

Install the dependencies:

```bash
npm i
```

Run the development server:

```bash
npm start
```

You can view the development server at [http://localhost:4001](http://localhost:4001).

### Production build

```bash
npm run build
```

### Where to add your code

Here are the main files and folders you will be working with:

#### Assets and Images

Add your assets and images into `src/assets/` folder. These will be copied into `dist/` folder as is

#### HTML

Add your custom HTML code into template `src/html/content.html`, this file will be added as innerHTML of the `body` element in templae `src/html/_index.html` file. This will be compiled into `dist/index.html`.

#### CSS

CSS is being compiled using SASS. Add your custom SASS code into template `src/sass/content.scss`, this will be compiled into `dist/widget.css`.

#### JS

Add your custom JS code into js files in `src/js/`. Each file will be concatanated into `dist/widget.js`. Files are concatanated in the order they are listed in the folder.

#### JS Vendor Libs

To add vendor JS libraries that will be compiled into `dist/vendor.js` and `dist/vendor.css` update the following section in `webpack.common.js`:

```javascript
new MergeIntoSingleFilePlugin({
        files: {
            "vendor.js": [
                'node_modules/jquery/dist/jquery.min.js',
                'node_modules/@popperjs/core/dist/umd/popper.js',
                'node_modules/bootstrap/dist/js/bootstrap.js',
                'node_modules/d3/dist/d3.js',
            ],
            "vendor.css": [
                //nothing here yet
            ],
            "widget.js": [
                paths.src + '/js/**/*.js',
            ]
        }
    }),

```

##### JS Conventions

Please keep JS simple, clean and namespaced.

When adding new files "modules" use this as the template for your new module.

```javascript
//define namespace for your JS file
//window.Widgets = Widgets || {};  //  already defined in _namespace.js
window.Widgets.App = Widgets.App || {};

//define your function to use in your component
(function($, ns, componentsNs, document, window) {
    ns.version = '1.0.0';

    ns.selectorComponent = '.js-component';

    ns.init = function() {
        //initialize your class
    };

})(jQuery, Widgets.App, Widgets, document, window);

//define your behaviour how will this component will be added to DOM.
(function($, ns, componentsNs, document, window) {
    
    //watch for the component to be added to DOM
    componentsNs.watchDOMForComponent(`${ns.selectorComponent}`, ns.init);

})(jQuery, Widgets.App, Widgets, document, window);

```

