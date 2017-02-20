# Controls 

Controls placed in `/beAdmin/src/controls` folder. You will need controls if you want to create the input field, panel, modal window or something else and if you don't want to create it from scratch. 
It's recommended to use created controls because they configured, designed, debugged and ready to work. 
Before you create your own component for input data, pop-up or a similar functions, make sure that it isn't in `controls` folder. 

Include the controls in the parent component with: 
`import ComponentName from '../../controls/name_of_control'`

Use it: 

```
<ComponentName
    prop1='string'
    prop2={variable}
    prop3={boolean}
    prop4={Number}
/>

```


### Existing controls: 

**1. Form controls**

* Checkbox

![](/assets/screenshot-localhost 3000-2017-02-20-15-09-49.png)
* Multiple checkbox
![](/assets/2.png)

* Dropdown simple
![](/assets/3.png)


* Field description
![](/assets/4.png)


* Field group edit
![](/assets/5.png)


* Field group edit with key
![](/assets/6.png)


* Field group text
![](/assets/7.png)


* Field static multiple
![](/assets/8.png)


* Simple select
![](/assets/9.png)


* Switch checkbox
![](/assets/10.png)


You can see examples of using form controls on the next title of this documentation (`"Simple form on React"`).

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