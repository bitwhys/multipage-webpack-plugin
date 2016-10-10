# Problem

Currently to architecht a webpack configuration for multi page web applications, there are many requirements for managing all assets and entry points. 

- In a multipage application every rendered page corresponds to a webpack entry point.
- Each entry point will have some sort of `index.html` file _or_ a MVC framework specific server template (partial) which renders to html content.
  - May have different paths, may not even be in the same directory as the entry point.
  - Should contain _just_ the assets bundled for that entry.
  - You would have to create essentially a `html-webpack-plugin` for each entry however posses extra configuration challenges:
  
  An example for a Laravel 4 Application using Twig Templates

  ```
  const templatesFn = (modules, twigRoot, assetsRoot, shared) => {
    return Object.keys(modules).map((entryName) => {
      return new HtmlWebpackPlugin({
        template: `${assetsRoot}/webpack.template.hbs`, //path.resolve(__dirname, "./assets/webpack.template.hbs"),
        filename: `${twigRoot}/webpack-bundles/${entryName}.twig`,
        chunks: ['inline', 'vendors', entryName, `${shared}`]
      })
    });
  } 
  ```