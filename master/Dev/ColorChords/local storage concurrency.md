<iframe src="https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage" height=500 style="width: 100%;" id="iframe" loading="lazy"></iframe>


``` js
function storeState(state) {
	window.localStorage.setItem('state', state)
}

function retrieveState() {
	if (window.localStorage.get('state')) pubsub.publish('state retrieved', state);
}

function hydratePage(retrievedState) {
	state = retrievedState;
} 

pubsub.subscribe('state changed', storeState)
pubsub.subscribe('page loaded', retrieveState)
pubsub.subscribe('state retrieved', hydratePage)
```

#state #cache