<iframe src="https://www.dofactory.com/javascript/design-patterns/observer" height=500 style="width: 100%;"></iframe>
 

```javascript
function StateSubject() {
    this.handlers = []; 
}

StateSubject.prototype = {

	getIndex: function (observer) {
		this.handlers.indexOf(observer)
	},

    subscribe: function (fn) {
        this.handlers.push(fn);
    },

    unsubscribe: function (fn) {
        this.handlers = this.handlers.filter(
            function (item) {
                if (item !== fn) {
                    return item;
                }
            }
        );
    },

	notify: function (observer) {
		let observerIndex = this.getIndex(observer)
		this.handlers[observerIndex].notify(observerIndex)
	},

    fire: function (o, thisObj) {
        var scope = thisObj || window;
        this.handlers.forEach(function (item) {
            item.call(scope, o);
        });
    }
}

function run() {

    var clickHandler = function (item) {
        console.log("fired: " + item);
    };

    var StateSubject = StateSubject();

    StateSubject.subscribe(clickHandler);
    StateSubject.fire('event #1');
    StateSubject.unsubscribe(clickHandler);
    StateSubject.fire('event #2');
    StateSubject.subscribe(clickHandler);
    StateSubject.fire('event #3');
}
```

#designpatterns