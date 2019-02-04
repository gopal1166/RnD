Code splitting:

	bundling: 
		The process of importing files and merging them into a single file
	bundle:
		This bundle can then be included on a webpage to load an entire app at once.
		
	but as app grows bundle also grows, 
	incase of importing third party libraries the app takes time to load
	
	So instead of one large bundle, we split the bundle to chunks
	
	with this code splitting we can 'lazy-load' the components required by the user not the entire app
	
	we're not reduce the code. but we avoided code that may not be needed by the user
	
	so reduced the amount of code needed during initial load
	So dynamically improves performance
	
	import():
		Best way to code split
		
	syntax:
	
		without code-split:
			````
			import CompA from './CompA';
			```
		
		with code-split:
			import('filePath').then(promise => {
				promise.component 
			})
			
		
	lazy():
		using this we can import and use as a normal component
		
		import React, { lazy, } 
		syntax:
			const CompA = lazy(() => import('filePath')) 
		
	Suspense:
		If the module containing the OtherComponent is not yet loaded by the time MyComponent renders, we must show some fallback content while we’re waiting for it to load - such as a loading indicator. This is done using the Suspense component.
		
	syntax:
		<div>
			<Suspense fallback={<div>Loading...</div>}>
				<OtherComponent />
			</Suspense>
		</div>
		
		
	Error boundary:
		in case of poor network if the modules failed to load by the time parent module is rendered then we can show error message
		
		import MyErrorBoundary from './MyErrorBoundary';
		const OtherComponent = React.lazy(() => import('./OtherComponent'));
		const AnotherComponent = React.lazy(() => import('./AnotherComponent'));

		const MyComponent = () => (
		  <div>
		    <MyErrorBoundary>
		      <Suspense fallback={<div>Loading...</div>}>
			<section>
			  <OtherComponent />
			  <AnotherComponent />
			</section>
		      </Suspense>
		    </MyErrorBoundary>
		  </div>
		);
		
		
Route based code splitting:
	A good place to start is with routes.
	
	import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
	import React, { Suspense, lazy } from 'react';

	const Home = lazy(() => import('./routes/Home'));
	const About = lazy(() => import('./routes/About'));

	const App = () => (
	  <Router>
	    <Suspense fallback={<div>Loading...</div>}>
	      <Switch>
		<Route exact path="/" component={Home}/>
		<Route path="/about" component={About}/>
	      </Switch>
	    </Suspense>
	  </Router>
	);
	
Named Exports:
	React.lazy currently only supports default exports
	If the module you want to import uses named exports, you can create an intermediate module that reexports it as the default. 
	
	// ManyComponents.js
	export const MyComponent = /* ... */;
	export const MyUnusedComponent = /* ... */;
	
	// MyComponent.js
	export { MyComponent as default } from "./ManyComponents.js";
	
	// MyApp.js
	import React, { lazy } from 'react';
	const MyComponent = lazy(() => import("./MyComponent.js"));
	
