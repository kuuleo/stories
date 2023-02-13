# I have Tailwind styled auth views

* [x] tailwindcss for the auth views

* [x] add this to `mix.exs`
```
{:tailwind, "~> 0.1", runtime: Mix.env() == :dev}
```

* [x] add this to `config.exs`
```
config :tailwind, version: "3.2.4", default: [
  args: ~w(
    --config=tailwind.config.js
    --input=css/app.css
    --output=../priv/static/assets/app.css
  ),
  cd: Path.expand("../assets", __DIR__)
]
```

* [x] add this to `mix.exs` to configure and alias to build CSS on deployment (only the tailwind default --minify part was added, esbuild and phx.digest was already there)
```
"assets.deploy": ["tailwind default --minify", "esbuild default --minify", "phx.digest"]
```

* [x] Enable watcher in development... add Tailwind to lis of watchers in `./config/dev.exs`
*added this directly under the esbuild watcher separated by a comma*
```
tailwind: {Tailwind, :install_and_run, [:default, ~(--watch)]}
```

* [x] run install command `mix tailwind.install` in root directory to create `./assets` directory and a `tailwind.config.js` file

* [x] configure template paths by adding these paths to `./assets/tailwind.config.js`
*left file unchanged after generation*
```
// See the Tailwind configuration guide for advanced usage
// https://tailwindcss.com/docs/configuration

let plugin = require('tailwindcss/plugin')

module.exports = {
  content: [
    './js/**/*.js',
    '../lib/*_web.ex',
    '../lib/*_web/**/*.*ex'
  ],
  theme: {
    extend: {},
  },
  plugins: [
    require('@tailwindcss/forms'),
    plugin(({addVariant}) => addVariant('phx-no-feedback', ['&.phx-no-feedback', '.phx-no-feedback &'])),
    plugin(({addVariant}) => addVariant('phx-click-loading', ['&.phx-click-loading', '.phx-click-loading &'])),
    plugin(({addVariant}) => addVariant('phx-submit-loading', ['&.phx-submit-loading', '.phx-submit-loading &'])),
    plugin(({addVariant}) => addVariant('phx-change-loading', ['&.phx-change-loading', '.phx-change-loading &']))
  ]
}
```

* [x] Tailwind directives to CSS
*they were added to top of file automatically... I left the Phoenix css there untouched... I like the way the toasts look so far... change them later if they get in the way*

* [x] remove default css import from `./assets/js/app.js`
*auto done by Tailwind*

I want to get down to basics.  I want to style using tailwind, a tag that looks like this:
```
<%= email_input f, :email, required: true class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-sky-300 focus:ring-sky-200" >
```

That code came from `new.html.heex` and it does not have a `~H"""..."""` it is like an html file except for the tags with the % in them and tag names that begin with a .

From the book, "The HEEEx templating engine is an extension of EEX. Just like EEx templates, HEEx will process template replacements within your HTML code."

... "Everything between the <%= and %> expressions is a template replacement and HEEx will evaluate the Elixir code within those tags and replace them with the result."


??HOW to style HEEx template replacement tags

...Because if I leave this tutorial like this it is like getting nothing done.  Have to have something to show for it, like the auth system I am actually using in production which includes presentable views with my logo

Or when using function components:

<.show_name name={@user.name} />

... I guess the .show if a function component...??

* [x] add tailwind-elements using npm from the assets directory

* [x] include the plugin require for tailwind-elements in the tailwind.config file

WHEN I uncheck the backgroung 100% 100% then the background toggles all the way to the right... ??WHAT is writing this:
```
[type="checkbox"]:checked
```

I did keep some phoenix classes... * [ ] see if the app.css will give me a hint

... this is WHAT it looks like:
```
[type='checkbox']:checked,[type='radio']:checked {
  border-color: transparent;
  background-color: currentColor;
  /*! background-size: 100% 100%; */
  background-position: center;
  background-repeat: no-repeat;
}
```

that 3rd attribute is commented out because I unchecked the box in the inspector
