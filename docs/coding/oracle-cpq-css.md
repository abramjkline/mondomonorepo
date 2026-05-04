# Oracle CPQ UI Tips

## General

One of the first things that you will notice when opening a new Oracle CPQ instance is the outdated appearance of the UI. Thankfully, it is possible to update the out-of-the-box styling. Some quick and simple updates can give the interface a much more modern look and help to align your instance with your overall brand.

There is a good deal of style updating that you can do in an Oracle CPQ instance from within the Oracle CPQ GUI. However, I have found some limitations to using the native system settings for styling the UI. This page contains some workarounds and tips that I've come up with for updating the styling for an Oracle CPQ instance. 

## Version Control

One thing that I recommend for any Oracle CPQ instance is to implement version control wherever possible. For the CSS, this means uploading your CSS files to the images directory where you can reference them throughout your Oracle CPQ application. 

The CSS files that come standard are: jetUI.css, alt_nav_menu.css, and nav_menu.css. In the GUI, these are referenced in the Stylesheet section. In order to implement version control, you'll need to follow these steps:

1. Download each of these files to get the current CSS.
2. Upload these files to your images directory under File Manager (I create a /css subdirectory, but you can put them really anywhere you want)
3. Create new files for each of the CSS files downloaded in step 1. 
4. In each of these files, add a single `@import` pointing to the versioned copy you uploaded in step 2:

    ``` css
    /* jetUI.css */
    @import url('../../image/css/jetUI.css');
    ```

    ``` css
    /* alt_nav_menu.css */
    @import url('../../image/css/alt_nav_menu.css');
    ```

    ``` css
    /* nav_menu.css */
    @import url('../../image/css/nav_menu.css');
    ```

5. Using the Oracle CPQ GUI, replace the files from step 1 with the new files created in step 3.

At this point, your CSS is being driven off of the files uploaded to the File Manager in step 3.

Oracle CPQ has a CLI tool that can be used to interact with the files in your instance, however, I have had little luck using this. Instead, I have been using a VS Code Extension called [CPQ DevKit](https://marketplace.visualstudio.com/items?itemName=CPQConsultant.cpq-devkit-o). You can configure the extension to pull from different environments (prod, dev, test). Using the extension, you can pull all of the files in the File Manager as well as all BML, Tables, and Assets included in your instance. This functionality allows you to version control any updates to your CSS files and beyond.

## Colors

It can be helpful to add your brand pallette to the root of your Oracle CPQ instance. This will make the color pallette easily accessible while coding. In order to do this, I created a file called ui_color_definitions.css where I defined all of the colors based on the brand guidelines and uploaded to the /css directory of my File Manager.

``` css
    :root {

        /* example color definitions */
        --header-color: #FF6E42;
        --button-color: #b1bacb;
        --button-color-hover: #b1bcab;

    }
```

Once you have defined these colors and uploaded the file, you can reference this ui_definitions.css file at the top of your other CSS files. In practice, code will look something like the snippet below.

``` css

    .button-middle {
        background: var(--button-color);
    }

    .button-middle:hover {
        background: var(--button-color-hover);
    }

    /* in some scenarios you may need to use !important to override system settings */
```

## Icons

The icons that come with Oracle CPQ leave quite a bit to be desired. Thankfully, there are many open-source icon libraries available that you can utilize to enhance the UI for your instance. I like to use the [Material Icon library](https://fonts.google.com/icons) to give my Oracle CPQ instance a nice, modern aesthetic. There are a ton of options for icons and you can customize icon color and size as well as choosing filled or outlined.

## Fonts

Oracle CPQ supports custom web fonts via CSS. You can load any font from [Google Fonts](https://fonts.google.com) by adding an `@import` to the top of your versioned CSS file and then applying it via `font-family` rules.

``` css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

body, .ui-widget {
    font-family: 'Inter', sans-serif;
}
```

As with colors, defining fonts once at the root level and referencing them throughout keeps your CSS maintainable as the instance grows.
