# Controls 

Controls place in `/beAdmin/src/controls` folder. You will need controls if you want to create the input field, panel, modal window or something else and if you don't want to create it from scratch. 
It's recommended to use created controls because they configured, designed, debugged and ready to work. 
Before you create your own component for input data, pop-up or a similar functions, make sure that it isn't in `controls` folder. 

Include the controls in the parent component with: 
`import ../../controls/name_of_control`

Use it: 

```
<Component_name
    prop1='string'
    prop2={variable}
    ...
    propN=Number
/>

```


### Existing controls: 

**1. Form controls**

Checkbox
Multiple checkbox
Dropdown simple
Field description
Field group edit
Field group edit with key
Field group text
Field static multiple
Simple select
Switch checkbox

**2. Pannels**
Modal
Modal zone
Panel box
Panel edit
Panel grid
Panel view 
Panel widget

**3. Other**

Content header
Datatable
Notification
Progressbar
Dropzone images