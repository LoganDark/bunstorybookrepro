# Storybook 8.2.0 introduced a regression

## How to reproduce

1. Install latest Bun
2. Run `bun install`
3. Run `bun storybook`
4. Load <http://localhost:6006> in browser
5. Storybook server immediately crashes:
   ```
   16585 |     path$n.dirname(nearestPackage.dir),
   16586 |     packageCache
   16587 |   ));
   16588 | }
   16589 | function loadPackageData(pkgPath) {
   16590 |   const data = JSON.parse(fs__default.readFileSync(pkgPath, "utf-8"));
           ^
   EISDIR: [postcss] Is a directory
      errno: -21
      code: "
         @font-face {
           font-family: 'Nunito Sans';
           font-style: normal;
           font-weight: 400;
           font-display: swap;
           src: url('./sb-common-assets/nunito-sans-regular.woff2') format('woff2');
         }
   
         @font-face {
           font-family: 'Nunito Sans';
           font-style: italic;
           font-weight: 400;
           font-display: swap;
           src: url('./sb-common-assets/nunito-sans-italic.woff2') format('woff2');
         }
   
         @font-face {
           font-family: 'Nunito Sans';
           font-style: normal;
           font-weight: 700;
           font-display: swap;
           src: url('./sb-common-assets/nunito-sans-bold.woff2') format('woff2');
         }
   
         @font-face {
           font-family: 'Nunito Sans';
           font-style: italic;
           font-weight: 700;
           font-display: swap;
           src: url('./sb-common-assets/nunito-sans-bold-italic.woff2') format('woff2');
         }
       "
    syscall: "read"
         fd: 3
   
         at readFileSync (native:1:1)
         at loadPackageData (C:\Users\LoganDark\bunstorybookrepro\node_modules\vite\dist\node\chunks\dep-BzOvws4Y.js:16590:39)
         at tryCleanFsResolve (C:\Users\LoganDark\bunstorybookrepro\node_modules\vite\dist\node\chunks\dep-BzOvws4Y.js:46292:23)
         at tryFsResolve (C:\Users\LoganDark\bunstorybookrepro\node_modules\vite\dist\node\chunks\dep-BzOvws4Y.js:46226:15)
         at C:\Users\LoganDark\bunstorybookrepro\node_modules\vite\dist\node\chunks\dep-BzOvws4Y.js:46048:19
         at resolveId (C:\Users\LoganDark\bunstorybookrepro\node_modules\vite\dist\node\chunks\dep-BzOvws4Y.js:45973:25)
         at C:\Users\LoganDark\bunstorybookrepro\node_modules\vite\dist\node\chunks\dep-BzOvws4Y.js:48919:17
         at processTicksAndRejections (unknown:12:39)
   Sourcemap for "/virtual:/@storybook/builder-vite/setup-addons.js" points to missing source files
   Sourcemap for "/virtual:/@storybook/builder-vite/vite-app.js" points to missing source files
   
   Bun v1.1.26 (Windows x64)
   error: script "storybook" exited with code 1
   ```

## How to fix

1. Open `package.json`
2. Change storybook version to `8.1.11`
3. Run `bun install`
4. Run `bun storybook`
5. Open <http://localhost:6006> in browser
6. Storybook server does not crash