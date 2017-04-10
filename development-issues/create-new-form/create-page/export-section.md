## 'Export' section

**'Export' section** includes description of React components which will be used with props and actions getting by [Relay Binding section](./relay-binding-section.md).
1. Wrap your imported React component \(in our example it's **'AchEdit'**\) in the described RelayBinding element:  
   `const AchEditPage = RelayBinding(AchEdit)`  
   It will be imported by default:   
   `export default AchEditPage;`

2. In this example we also use the form in the modal window. So, constant "AchEditModal" describes the form with the ModalZone wrapper.

```javascript
export const AchEditModal = RelayBinding((props) => {
  let { locale } = props;
  return (
    <ModalZone locale={ locale }>
      <AchEdit {...props }/>
    </ModalZone>
  )
})
```

The page is ready to use.

