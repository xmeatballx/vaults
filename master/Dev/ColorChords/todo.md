
## In Progress
- [ ] get rid of this.actives and just use this.colors??
- [ ] comment source code for documentation
	- [ ]  chords
	- [x]  palette
	- [ ]  piano
	- [ ]  controller
	- [ ]  theme 
	- [ ]  params
	- [ ]  app
---

## Current
- [ ]  fix piano styling
	- [x]  keep piano max-width equal to app container max-width
	- [ ]  deal with svg line doubling between octaves
- [ ]  avoid rerendering whole palette when possible
	- [x]  create each colorblock once and remove from dom when disposed
	- [ ]  use ref from event callback to update component view and cache when changed
	- [ ]  in what cases is a complete rerender required?
- [ ]   adjust colorblock text for contrast based on bg color
- [x] implement sortable on palette
	- [x] use the old/new index from sortable update to rearrange colors array
- [ ] maybe get rid of hold. it doesnt make sense replace with tutorial
---

## Down the Line
- [ ] implement local storage concurrency
---
 
 ## Maybes
 - [ ] Using theme pub sub channel add option to assign colors to css theme variables
	- [ ] implement themehandler module in the controller directory

---

## Trash
- [x] add note sorting
	- [x] add sort button to avoid confusing autosorting
- [x] experiment with 180deg arc instead of circle
- [x] experiment with accurate color wheel instead of hsv picker

## Completed
- [x]  add keyboard input for musical keys
- [x] implement octave control
- [x] finish chord picker
- [x] make transpose slider update piano
- [x] change trash icon to svg so color can transition on theme toggle
- [x] implement tab switcher functionality
	- [x] color only view
	- [x] toggle icon color active on tab change
	- [x] code view
		- [x] extract rgb value
		- [x] extract hsv value [[useful snippets#RGBtoHSV]]
		- [x] extract hex code [[useful snippets#RGBtoHex]]
	- [x] info
		- [x] write explanation
		- [x] implement modal over focus container
- [x] Change innerHTML string templates to document fragments for security and optimization
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
	- [x] add createNote factory and createShaderUniforms factory [[factorypattern]]
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