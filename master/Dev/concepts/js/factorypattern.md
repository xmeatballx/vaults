```js
const Laptop = function({ ram, hdd, name }) {  
  this.ram = ram || 0;  
  this.hdd = hdd || 0;  
  this.name = name || "";  
};module.exports = Laptop;
```

instantiate with 
```js
const newLaptop = Laptop({
	ram: "64gb",
	hdd: "SSD",
	name: "Lenovo"
})
```