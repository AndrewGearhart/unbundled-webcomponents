## unbundled webcomponents
This is an optimized workflow for those implementing unbundled builds for web components. The goal is to provide the easiest integration for unbundled builds, made popular by CDNs in large organizations.

### Why unbundled
- If you are using a CDN approach where elements power multiple sites
- If you build your app as if there is unbundled references and want to leverage optimizations as a result
- If you are using a CMS or application that controls its own JS via a different workflow, this is probably the safer option
- This is a stepping stone to the future. In the next few years unbundling will be possible without tooling thanks to importmaps
- Your running an HTTP/2 server / CDN and know it's faster!

### Why not to unbundle
- anti-pattern in the JS community of today
- still uses `polymer build` to keep things separate
- webpack / rollup by themselves will make smaller asset bundles and your shipping 1 stand alone app as opposed to several sites across a CDN

## Tools in here
This has a configuration of polymer.json, a format used by the polymer CLI in order to create 3 builds of your assets.
- es6+ - This is labeled es6 but is running es8 capable build which all Evergreen browsers support
- es6-amd - a few rare versions of Safari and many older versions of Firefox could handle ES6 spec but NOT `import`
- es5-amd - compiled to work on IE11, older versions of Edge, Firefox and Safari

## How does it work?
The file in `integrations/build.js` does feature detection in order to establish if this is an ESM capable platform or needs a different build at run time. This reduces the integration with your platform / CMS / application down to two lines of `<script>` tags. The 1st adds support for CDNs as well as an option for `forceUpdate` which if the browser can't serve the build.js file it will force the user to a page asking them to upgrade.

We feature detect `import()` which 90+% of traffic supports as of end of 2019 and inject ES module based `<script type="module">` imports. From there we try and detect which polyfills are needed based on the platform.

It has been heavily battle tested and is used in production in mutliple domains and websites.

## Who dis
This approach was developed by Penn State and tested by The US National Archives for accuracy.