
## In Progress

---

## Current

- [ ] add note sorting
	- [ ] add sort button to avoid confusing autosorting

---

## Down the Line
- [ ] experiment with 180deg arc instead of circle
- [ ] experiment with accurate color wheel instead of hsv picker
- [ ] Using theme pub sub channel add option to assign colors to css theme variables
	- [ ] implement themehandler module in the controller directory
- [ ] implement tab switcher functionality
	- [ ] color only view
	- [ ] code view
		- [ ] extract rgb value
		- [ ] extract hsv value [[useful snippets#RGBtoHSV]]
		- [ ] extract hex code [[useful snippets#RGBtoHex]]
	- [ ] info
		- [ ] write explanation
		- [ ] implement modal over focus container
- [ ] implement local storage concurrency

 ---

## Completed
- [x] fix select focus styling
- [x] add delete button
- [x] fix transpose display to step over semitones instead of degrees
- [x] extract controls template into individual components
- [x] refactor js file structure (MVC maybe?) [[MVC]]
- [x] fix missing top divider on tab switcher aside
- [x] scrap all curtains code and just use canvas
- [x] implement curtains shader
	- [x] explore making shader canvases web components
	- [x] implement main graphic
	- [x] implement getting color from pixels
- [x] implement addNote function
	- [x] add createNote factory and createShaderUniforms factory [[Dev/concepts/js/factorypattern]]
	- [x] initialize state with createNote and createShaderUniforms factories
	- [x] implement button on click useAdd function and addNote functions
- [x] FIX UL WIDTH OVERFLOW
- [x] implement useTheme function for dark/light switching
- [x] application architecture [[application flow graph]]
- [x] implement state module
- [x] implement event handler
- [x] implement pubsub 
- [x] implement template rendering
- [x] update slider UI values on input not change
- [x] implement new piano code