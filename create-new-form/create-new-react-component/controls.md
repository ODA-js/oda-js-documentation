# The Controls 

The controls placed in `/beAdmin/src/controls` folder. You will need controls if you want to create the input field, panel, modal window or something else and if you don't want to create it from scratch. 
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

####1. Form controls
___
**Checkbox**

![](/assets/1.png)
___
**Multiple checkbox**

![](/assets/2.png)
___

**Dropdown simple**

![](/assets/3.png)
___

**Field description**

![](/assets/4.png)
___

**Field group edit**

![](/assets/5.png)
___


**Field group edit with key**

![](/assets/6.png)
___

**Field group text**

![](/assets/7.png)
___

**Field static multiple**

![](/assets/8.png)
___

**Simple select**
![](/assets/9.png)
___

**Switch checkbox**

![](/assets/10.png)

___

You can see examples of using form controls on the next title of this documentation (`"Simple form on React"`).

####**2. Pannels**
**Modal**
![](/assets/111.png)
___

**Panel box**
![](/assets/122.png)
___

**Panel edit**
![](/assets/444.png)
___

**Panel grid**
___

**Panel view **
___

**Panel widget**
![](/assets/555.png)
___
####**3. Other**

Content header
Datatable
Notification
Progressbar
Dropzone images