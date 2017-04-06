# Controls

The controls are placed in `/beAdmin/src/controls` folder. You will need the controls if you want to create the input field, panel, modal window or something else and if you don't want to create them from scratch.  
It's recommended to use created controls because they are configured, designed, debugged and ready to work.

Before you create your own component for input data, pop-up or a similar functions, make sure that it isn't in `controls` folder.

Include the controls in the parent component with:  
`import ComponentName from '../../controls/name_of_control'`

Use this:

```
<ComponentName
    prop1='string'
    prop2={variable}
    prop3={boolean}
    prop4={Number}
/>
```

### Existing controls:

#### 1. Form controls

---

**Checkbox**

![](/assets/1.png)

---

**Multiple checkbox**

![](/assets/2.png)

---

**Dropdown simple**

![](/assets/3.png)

---

**Field description**

![](/assets/4.png)

---

**Field group edit**

![](/assets/5.png)

---

**Field group edit with key**

![](/assets/6.png)

---

**Field group text**

![](/assets/7.png)

---

**Field static multiple**

![](/assets/8.png)

---

**Simple select**  
![](/assets/9.png)

---

**Switch checkbox**

![](/assets/10.png)

---

You can see the examples of using the form controls in the next title of this documentation \(`"Simple form on React"`\).

#### **2. Panels**

**Modal**  
![](/assets/111.png)

---

**Panel box**  
![](/assets/122.png)

---

**Panel edit**  
![](/assets/444.png)

---

**Panel widget**  
![](/assets/555.png)

---

#### **3. Other**

**Content header**  
![](/assets/11.png)

---

**Datatable**

![](/assets/114.png)

---

**Notification**

For using notification - need binding redux notification \(see **Create Page/Relay Binding section** && **Add Global variables**\)

---

**Progress bar**  
![](/assets/112.png)

---

**Dropzone images**

![](/assets/113.png)

---

