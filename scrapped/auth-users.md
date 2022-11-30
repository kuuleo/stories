# As a user, I can sign in and sign out of my account

* [ ] loginRequest action
* [ ] loginSuccess action
* [ ] loginFailure action

* [ ] loginRequest action triggers http post request to

* [ ] loginSuccess action triggers authReducer to save authData to authSlice
* [ ] loginFailure action triggers authReducer to clear authData from authSlice

REF Angular service is just an object which delivers a set of context-independent methods

In object oriented languages such as C++, it is not possible to create an object.  In those type of languages, a class is created and then classes create objects.  Since I can create objects directly in Javascript simply by saying `let myObject = {}`, create objects instead of classes for services.

* [x] create an object for the auth service
* [ ] don't give it any properties since all data will be kept in the state
* [ ] make a function inside the object for each request used for authentication


## MP20 get all the request routes into a service
* [ ] first put login format `http://localhost:3000/THE_PATH`
* [ ] check that one works this way first (start with login)
* [ ] then put all of them in this format `${environment.api_url}/THE_PATH`
* [ ] test that they all work

## MP20 get the actions showing up in the redux dev tools
* [x] find the REF for redux nextjs
*??WHICH example app is it in the drifter.live directory?
---> ~/Development/tutorials/redux-123456*
* [x] add these dependencies:
```
"next-redux-wrapper": "^8.0.0",
"react-icons": "^4.4.0",
"react-redux": "^8.0.4",
"redux": "^4.2.0",
"redux-devtools-extension": "^2.13.9",
"redux-thunk": "^2.4.1"
```

## I just assumed that react-redux is observable based just like ngrx
### ... but I guessed wrong
### ... and I still want to use observables
*Since that is WHAT I spent the last 2 years learning by learning ngrx...*
## MP20 use observables with react-redux
* [x] install next-redux-wrapper... I did that in the above WHEN I added the stuff from redux-123456
*This `REF: https://medium.com/@m.quintal/using-redux-observable-on-nextjs-5b6c0d57ce81` says to use the following dependency for redux-observable*
* [ ] install next-redux-observable
* [ ] use withObservable on `pages/_app.ts`
* [ ] use resolvedActions on pages components
* [ ] provide which actions need to be loaded on that particular page
* [ ] install @reduxjs/toolkit based on createStore being deprecated

*MIND so first if I'm doing just the wrapper, the gist is wrap the store with a provider component like the following:*
```
<Provider...
```

* [ ] redux-observable
* [ ] observable-hooks

(that guy with crazy strict section) says this is the simples configuration for observable-hooks
*... using a single centralized store at the app level*
```
const store: Store<State> = createStore<State, Action<AppAction>, undefined, undefined>(reducer, initialState);
```

and since I want to use redux toolkit instead...

```
const store: Store<State> = createStore<State, Action<AppAction>, unknown, unknown>(reducer, initialState, applyMiddleware(logger));
```

*blah blah blah*

Bottom line, I have to get the store connected to a component someHOW...

* [x] copy the entire store from the following REF
*REF ---> https://github.com/enhsu/Next-redux-observable*
* [ ] first just getting it working as it is in his demo
*that just means a list of names on the screen and a counter that counts
... and redux dev tools where I can see the actions trigger and the state*
* [ ] modify my app so that the store is loaded in `_app.tsx`






* [ ] move the validation logic out of the forms and into a utility file of some kind

* [ ] do the entire authentication process using plain devise
* [ ] make the template that has the react entry component only accesable if user is authenticated
