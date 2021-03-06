# A modern Front End development environment

This is a development manual for a digital agency called Dude (Digitoimisto Dude Oy), [check out the company website](https://www.dude.fi) where [@ronilaukkarinen](https://github.com/ronilaukkarinen) is the head of technical development at the moment. Dude is using plenty of tools, apps, modules, frameworks which together are called "stack". Dudestack-instructions contains information about these tools *and* instructions on how to set up a similar stack.

This wiki and instructions exist only because Dude's envinroment setup is growing in a fast pace and there's simply too many repositories to consider when building the stack from scratch.

The instructions assume that you don't have *anything* pre-installed. If you have something installed, please just skip the step. Scroll down to [Installation](https://github.com/digitoimistodude/dudestack-instructions#installation).

We hope you enjoy!

## Table of contents

1. [Setting up](#setting-up)
3. [Requirements](#requirements)
3. [Install requirements](#install-requirements)
4. [Install macOS LEMP (preferred)](#install-macos-lemp-preferred)
5. [Install Vagrant (optional)](#install-vagrant-optional)
6. [Install dudestack](#install-dudestack)
7. [Install devtools (optional)](#install-devtools-optional)
8. [Install starter theme](#install-starter-theme)
9. [How to generate local site specific HTTPS certificates (optional)](#how-to-generate-local-site-specific-https-certificates-optional)
10. [Building blocks for SCSS, jQuery, PHP](#building-blocks-for-scss-jquery-php)
    1. [For building](#for-building)
    2. [For developing and designing](#for-developing-and-designing)
        1. [Layout](#layout)
        2. [Typography](#typography)
        3. [Effects](#effects)
        4. [WordPress-themes](#wordpress-themes)
        5. [Freebies](#freebies)
        6. [Inspiration and useful parts](#inspiration-and-useful-parts)
    3. [For testing and debugging](#for-testing-and-debugging)
    4. [Other apps and tools included in daily workflow](#other-apps-and-tools-included-in-daily-workflow)

### Setting up

These will be installed if you follow the instructions:

- Vagrant LEMP environment with [marlin-vagrant](https://github.com/digitoimistodude/marlin-vagrant) (use if you prefer Vagrant)
- macOS native LEMP environment (Homebrew) [macos-lemp-setup](https://github.com/digitoimistodude/macos-lemp-setup) (use if you prefer native approach without VM)
- WordPress stack with [dudestack](https://github.com/digitoimistodude/dudestack) (based on [roots/bedrock](https://github.com/roots/bedrock))
- Gulp, nodejs and npm-modules with [devpackages](https://github.com/digitoimistodude/devpackages)
- Landing pages with [modern-html5-boilerplate](https://github.com/digitoimistodude/modern-html5-boilerplate)

## Install requirements

1. Install latest version of [XCode](https://developer.apple.com/xcode/downloads/) to get necessary utils. Apple's XCode development software is used to build Mac and iOS apps, but it also includes the tools you need to compile software for use on your Mac. XCode is free and you can also find it in the [App Store](https://itunes.apple.com/us/app/xcode/id497799835?mt=12).
2. Install Xcode Command Line Tools by running 'xcode-select --install'
3. Install 
. Open **Terminal** and run `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"` to download latest version of [Homebrew](http://brew.sh/)
4. Run `brew install caskroom/cask/brew-cask` to get [Homebrew Cask](https://formulae.brew.sh/cask/)
5. Install latest version of [rvm](https://rvm.io/) with `curl -L https://get.rvm.io | bash -s stable --auto-dotfiles --autolibs=enable --rails` to get ruby working
6. Install latest version of [Git](http://git-scm.com/downloads) with `brew install git`
7. Install latest version of [Composer](https://getcomposer.org) with `curl -sS https://getcomposer.org/installer | php && sudo mv composer.phar /usr/local/bin/composer && sudo chmod +x /usr/local/bin/composer`

## Install macOS LEMP (preferred)

Follow [the Installation instructions of native LEMP components on Mac](https://github.com/digitoimistodude/macos-lemp-setup)

## Install Vagrant (optional)

Follow [the Installation instructions of our Vagrant box](https://github.com/digitoimistodude/marlin-vagrant#installation-on-maclinux).

## Install dudestack

1. Clone [dudestack](https://github.com/digitoimistodude/dudestack) to your Projects directory with `cd ~/Projects && git clone https://github.com/digitoimistodude/dudestack`
15. Run `cd ~/Projects/dudestack && sh bin/setup.sh` and complete the setup process
17. Run `createproject` and wait the script to run through. **Note:** It's intended that every project name is one word, written in lowercase.

## Install devtools (optional)

If you want to use your own Gulpfile, Gruntfile, bower, etc, in this point you are practically done. **Congratulations!** However, if you want to use dudestack-packages, please continue reading.

18. Go to your project directory by `cd ~/Project/projectname` and clone [devpackages](https://github.com/digitoimistodude/devpackages) with `git clone https://github.com/digitoimistodude/devpackages .` (note the dot in the end of a command, we want these to the same directory)
19. Edit `PROJECTNAME` (project folder name) and `THEMENAME` (your theme folder name in content/themes/x) to match your WordPress project and theme name sin **gulpfile.js** and **package.json**.
20. Install [Node.js](http://nodejs.org/) with `brew install node`
21. Install npm updates checker [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) with `sudo npm install -g npm-check-updates`
22. Check updates for npm modules by running `npm-check-updates -u` (still in the Project directory, /Users/yourusername/Projects/yourproject. You can check where you are by `pwd`)
23. Install npm package updates by `npm install` and update them by `npm update`
25. Run `gulp watch`. A new browser window should open and you can start coding your WordPress theme.
26. If you want to create a landing page instead, go to Project dir with `cd ~/Projects`, clone [modern-html5-boilerplate](https://github.com/digitoimistodude/modern-html5-boilerplate) with `git clone https://github.com/digitoimistodude/modern-html5-boilerplate`, rename folder to your project, edit **gulpfile.js** and start coding

## Install starter theme

Follow [the Installation instructions in air theme repository](https://github.com/digitoimistodude/air#installation).

## How to generate local site specific HTTPS certificates (optional)

1. First, create a `~/Certificates` directory to your $HOME.

2. `cd ~/Certificates`, then generate a key (replace `PROJECTNAME` with your actual project name that you defined in `createscript` process: 

```` bash
openssl genrsa -des3 -passout pass:x -out PROJECTNAME.pass.key 2048 && openssl rsa -passin pass:x -in PROJECTNAME.pass.key -out PROJECTNAME.test.key && rm PROJECTNAME.pass.key
````

2. Then, generate a certificate based on that key:

```` bash
openssl req \
    -key PROJECTNAME.test.key \
    -x509 \
    -nodes \
    -new \
    -out PROJECTNAME.test.crt \
    -subj /CN=PROJECTNAME \
    -reqexts SAN \
    -extensions SAN \
    -config <(cat /System/Library/OpenSSL/openssl.cnf \
        <(printf '[SAN]\nsubjectAltName=DNS:PROJECTNAME')) \
    -sha256 \
    -days 3650
````

3. Then create one for localhost (BrowserSync):

```` bash
openssl genrsa -des3 -passout pass:x -out localhost.pass.key 2048 && openssl rsa -passin pass:x -in localhost.pass.key -out localhost.key && rm localhost.pass.key
````

```` bash
openssl req \
    -key localhost.key \
    -x509 \
    -nodes \
    -new \
    -out localhost.crt \
    -subj /CN=localhost \
    -reqexts SAN \
    -extensions SAN \
    -config <(cat /System/Library/OpenSSL/openssl.cnf \
        <(printf '[SAN]\nsubjectAltName=DNS:localhost')) \
    -sha256 \
    -days 3650
````

4. Open **Keychain Access** app from macOS Launchpad. Click *Certificates*, then *File > Import Items...*, navigate to *Certificates* directory and select your crt file. Double click added Self-signed root certificate, select **Trust** and choose **Always Trust** in *When using this certificate:* selection. Make sure all dropdowns are **Always Trust**. Close box, add your password and press *Update Settings* button. Do the same for localhost.

5. Change browserSync part of gulpfile.js to match this (with your own username of course):

````
  browserSync.init(files, {
    proxy: "https://PROJECTNAME.test",
    notify: true,
    browser: "Chromium",
    https: {
      key: "/Users/rolle/Certificates/localhost.key",
      cert: "/Users/rolle/Certificates/localhost.crt"
    }
  });
````

Please note: You don't need to do localhost after first time, once is enough.

6. Change your siteurl and homeurl protocols to https in your `.env` file:

````
WP_HOME=https://PROJECTNAME.test
WP_SITEURL=https://PROJECTNAME.test/wp
````

7. Update your [marlin-vagrant](https://github.com/digitoimistodude/marlin-vagrant) or [macos-lemp-setup](https://github.com/digitoimistodude/macos-lemp-setup) vhost like this:

````
server {
    listen 443 ssl http2;
    root /var/www/PROJECTNAME;
    index index.php;    
    server_name PROJECTNAME.test;

    include php7.conf;
    include global/wordpress.conf;

    ssl_certificate /Users/rolle/Certificates/PROJECTNAME.test.crt;
    ssl_certificate_key /Users/rolle/Certificates/PROJECTNAME.test.key;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    ssl_dhparam /etc/ssl/certs/dhparam.pem;
    ssl_ciphers 'ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA';
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_stapling_verify on;
    add_header Strict-Transport-Security max-age=15768000;
}

server {
    listen 80;
    server_name PROJECTNAME.test;
    return 301 https://$host$request_uri;
}
````

8. Run `sudo nginx -t` to test nginx settings (on [macos-lemp-setup](https://github.com/digitoimistodude/macos-lemp-setup)) and restart your nginx service.

### Building blocks for SCSS, jQuery, PHP

You will need a WordPress theme, User Interface or website base, so I have collected some useful bits and pieces below.

#### For building

- [BitBucket](https://bitbucket.org/) - Bitbucket is a free code DVCS hosting site for Git and Mercurial. Manage your development with a hosted wiki, issue tracker and source code.
- [Homebrew](http://brew.sh/) - The missing package manager for macOS
- [Homebrew Cask](http://caskroom.io/) - Homebrew Cask extends Homebrew and brings its elegance, simplicity, and speed to macOS applications and large binaries alike.
- [RVM](https://rvm.io/) - RVM is a command-line tool which allows you to easily install, manage, and work with multiple ruby environments from interpreters to sets of gems.
- [Node.js](http://nodejs.org/) - Node.js® is a platform built on Chrome's JavaScript runtime for easily building fast, scalable network applications.
- [npm](https://www.npmjs.com/) - A package manager for node/browsers/gulp/etc.
- [Vagrant](https://www.vagrantup.com/) - Create and configure lightweight, reproducible, and portable development environments.
- [Vagrant Manager](http://vagrantmanager.com/) - Manage your vagrant machines in one place with Vagrant Manager for macOS.
- [Gulp](http://gulpjs.com/) - Automate and enhance your workflow (my gulpfile.js can be found in [devpackages](https://github.com/digitoimistodude/devpackages))
- [BrowserSync](http://www.browsersync.io/) - Time-saving synchronised browser testing. (included in Gulp like in many other awesome tasks, check out my [devpackages](https://github.com/digitoimistodude/devpackages))
- [Bower](http://bower.io/) - A package manager for the web (to install and update CSS/Javascript packages and their dependencies, see my [devpackages](https://github.com/digitoimistodude/devpackages))
- [Composer](https://getcomposer.org/) - Dependency Manager for PHP
- [WP-CLI](http://wp-cli.org/) - A command line interface for WordPress
- [Google Chrome Canary](https://www.google.com/chrome/browser/canary.html) - Google Chrome Canary has the newest of the new Chrome features.
- [Sublime Text 3](http://www.sublimetext.com/3) - Sublime Text is a sophisticated text editor for code, markup and prose. (also check out current [sublime-settings](https://github.com/digitoimistodude/sublime-settings))
- [Atom](https://atom.io/) - The hackable text editor by GitHub. Check out [atom-settings](https://github.com/digitoimistodude/atom-settings)

#### For developing and designing

##### Layout

- [Jeet Grid System](http://jeet.gs/) - Smart CSS preprocessor grids
- [Normalize.scss](https://github.com/JohnAlbin/normalize-scss) - A modern, HTML5-ready alternative to CSS resets
- [Vide](http://vodkabears.github.io/vide/) - Easy as hell jQuery plugin for video backgrounds
- [jQuery.equalHeights](https://github.com/mattbanks/jQuery.equalHeights) - Simple equal heights jQuery plugin
- [Packery](http://packery.metafizzy.co/) - Packery makes your crazy & clever layout a real thing.
- [macy.js](https://github.com/bigbitecreative/macy.js) - A lightweight dependency-free JavaScript library designed to sort items vertically into columns by finding an optimum layout with a minimum height.
- [Magnific Popup](http://dimsemenov.com/plugins/magnific-popup/) - Magnific Popup is a responsive lightbox & dialog script with focus on performance and providing best experience for user with any device
- [fancyBox](http://fancyapps.com/fancybox/) - Fancy jQuery Lightbox Alternative

##### Typography

- [Typographic](https://github.com/corysimmons/typographic) - Easy SCSS or Stylus responsive typography with vertical rhythm, modular scale, font stacks, and more
- [Sass Boilerplate's fontFace](https://github.com/magnetikonline/sassboilerplate) - Easy include a webfont
- [knife](https://github.com/Pushplaybang/knife) - Nail vertical rhythm, modular scale, and REMs like a boss with this simple set of SASS/SCSS variables, functions and mixins.
- [Sassy-Gridlover](https://github.com/hiulit/Sassy-Gridlover) - Super easy to use Sass mixins to establish a typographic system with modular scale and vertical rhythm. (alternative)
- [Sassline](https://sassline.com/) - Set text on the web to a baseline grid with Sass & rems.

##### Effects

- [mo.js](https://github.com/legomushroom/mojs) - Motion graphics toolbelt for the web
- [Animate.css](http://daneden.github.io/animate.css/) - A cross-browser library of CSS animations. As easy to use as an easy thing.
- [WOW.js](http://mynameismatthieu.com/WOW/) - Reveal Animations When Scrolling
- [Slick](http://kenwheeler.github.io/slick/) - The last carousel you'll ever need
- [skrollr](http://prinzhorn.github.io/skrollr/) - Parallax scrolling for the masses
- [waypoints](http://imakewebthings.com/waypoints/) - Waypoints is the easiest way to trigger a function when you scroll to an element.
- [saffron](https://github.com/colindresj/saffron) - A simple Sass mixin library for animations and transitions

##### WordPress-themes

- [Air-light](https://github.com/digitoimistodude/air-light) - A minimalist WordPress theme starting point

##### Freebies

- [StockSnap.io](https://stocksnap.io/) - Beautiful free stock photos. (CC0)
- [TheStocks.im](http://thestocks.im/) - The best royalty free
stock photos in one place (CC0)
- [Pexels Videos](https://videos.pexels.com/) - Completely free stock videos. (CC0)
- [Pixel Buddha](http://pixelbuddha.net/) - Free and premium resources for designers and developers
- [Streetwill](http://streetwill.co/) - Free Hi-Res Photos (CC0)
- [Life of Pix](http://www.lifeofpix.com/) - Free high-resolution photos (CC0)

##### Inspiration and useful parts

- [CodyHouse](http://codyhouse.co/)
- [Codrops](http://tympanus.net/codrops/)
- [Codepen](http://codepen.io/)

#### Testing and debugging

- [caniuse-cmd](https://github.com/sgentle/caniuse-cmd) - [Caniuse](http://caniuse.com/) command line tool
- [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) - The PageSpeed tools analyze and optimize your site following web best practices.
- [GTMetrix](https://gtmetrix.com/) - GTmetrix gives you insight on how well your site loads and provides actionable recommendations on how to optimize it.
- [alix](https://github.com/ireade/alix) - Alix is a browser extension for a11y.css. It allows you to lint your HTML for Accessibility issues simply by applying a stylesheet that makes use of advanced CSS selectors.
- [tota11y](https://github.com/Khan/tota11y) - An accessibility (a11y) visualization toolkit
- [WAVE](https://wave.webaim.org/extension/) - Web accessibility evaluation tool

#### Other apps and tools included in daily workflow

Please let me know if you have suggestions for new/better apps/modules/plugins...

- [PixelSnap](https://getpixelsnap.com/) - The fastest way to measure everything on screen.
- [ColorSnapper](http://www.colorsnapper.com/) - The missing color picker for Mac
- [KeepingYouAwake](https://github.com/newmarcel/KeepingYouAwake) - Don't let your Mac fall asleep
- [Amphetamine](https://itunes.apple.com/us/app/amphetamine/id937984704?mt=12) - With Amphetamine, you can effortlessly override your energy saver settings and keep your Mac awake.
- [Trello](https://trello.com/ronilaukkarinen/recommend) - Trello is the free, flexible, and visual way to organize anything with anyone.
- [Todoist](http://todoist.com/) - Todoist is the best online task management app and to-do list.
- [f.lux](https://justgetflux.com/) - Is your computer keeping you up late? f.lux is free software that warms up your computer display at night, to match your indoor lighting.
- [ImageOptim](https://imageoptim.com/) - better Save For Web
- [Moom](http://manytricks.com/moom/) - Move and zoom windows
- [LittleIpsum](https://itunes.apple.com/us/app/littleipsum/id405772121?mt=12) - The best Latin text generator for macOS. Incredibly quick and lightweight. And it’s completely free!
