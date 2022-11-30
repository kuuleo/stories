# MP20 Create a bundled drifter app with NextJs or React inside of Rails app instead of running on a different server

There is a script in my rails package.json that uses esbuild to take all files form `app/javascript.`  It takes these files and bundles them and puts the bundled build in `app/assets/builds`.

CSS is done the same way.  It takes files from `./app/assets/stylesheets/application.tailwind.css` and outputs the css to `./app/assets/builds/application.css`

"To get the optimal loading performance in production, it is still better to bundle your code with tree-shaking, lazy-loading, and common chunk splitting (for better caching)" (REF vitejs.dev/guide/why.html)

# REF https://blog.dennisokeeffe.com/blog/2022-02-19-rails-7-using-react-with-esbuild

* [x] create new application with `rails new drifter -j esbuild --skip-jbuilder -d=postgresql`

* [x] mkdir app/javascript/components
* [x] vim `app/javascript/components/App.tsx`
```
import * as React from 'react'
import * as ReactDOM from 'react-dom'

interface AppProps {
  arg: string
}

const App = ({ arg }: AppProps) => {
  return <div>{`Hello, ${arg}!`}</div>
}

document.addEventListener("DOMContentLoaded", () => {
  const rootEl = document.getElementById("root")
  ReactDOM.render(<App arg="Rails 7 with EsBuild" />, rootEl)
})
```
* [x] bin/rails g controller components index

* [x] `app/javascript/application.ts`
```
import '@hotwired/turbo-rails'
import './components/App'
```

* [x] add div for React app to hook into in `app/views/components/index.html.erb`
```
<h1>Components#index</h1>
<div id="root"></div>
```

* [x] in `config/routes.rb` ad `root 'components#index'`

* [x] App.tsx is being rendered in Rails
