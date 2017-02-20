#Simple form on React

Typical React component looks like this: 
```javascript
import React from 'react';

import {
  compose,
  withProps
} from 'recompose';

import PanelEdit from '../../controls/panel_edit';

import Checkbox from '../../controls/checkbox';
import MultipleCheckbox from '../../controls/checkbox_many';
import DropdownSimple from '../../controls/dropdown_simple';
import FieldDescription from '../../controls/field_description';
import FieldGroupEdit from '../../controls/field_group_edit';
import FieldGroupEditWithKey from '../../controls/field_group_edit_with_key';
import FieldGroupText from '../../controls/field_group_text';
import FieldStaticMultiple from '../../controls/field_static_many';
import SimpleSelect from '../../controls/select_simple';
import SwitchCheckbox from '../../controls/switch_checkbox';

const PageAchEdit = ({ data, ui, actions, locale }) => {

  return(
    <PanelEdit>
      <PanelEdit.Header
        title={ui.title[locale]}
        closeLabel={ui.closeButton[locale]}
        onReset={actions.onReset}
      />
      <PanelEdit.Form
        onSubmit={actions.onSubmit}
        onReset={actions.onReset}
        btnSaveTitle={ui.saveChanges[locale]}
        btnCancelTitle={ui.cancel[locale]}
        colWidth={12}
        colOffset={0}
      >
        <h3>Checkbox</h3>
        <Checkbox
          name='name_checkbox'
          label='Checkbox label'
          value='true'
          onChange={(e)=>{e.preventDefault();}}
        />
        <h3>Multiple checkbox</h3>
        <MultipleCheckbox
          ui={ui.multipleCheckbox}
          value={['Num1', 'Num3']}
          list={['Num1', 'Num2', 'Num3']}
          locale={locale}
          onChange={(e)=>{e.preventDefault();}}
          fieldKey='key'
          fieldDisplay='value'
        />
        <h3>Simple dropdown</h3>
        <DropdownSimple
          title='num1-name'
          name="name-dropdown"
          data={[
            {
              "value":"num1",
              "name": "num1-name"
            },
            {
              "value":"num2",
              "name": "num2-name"
            },
            {
              "value":"num3",
              "name": "num3-name"
            }
          ]}
          onSelect={(e)=>{e.preventDefault();}}
        />
        <h3>Field description</h3>
        <FieldDescription
          text='text'
          title='title'
        />
        <h3>Simple Input</h3>
        <FieldGroupEdit
          name='group_edit_name'
          label='label'
          placeholder='placeholder'
          value='Value'
          labelWidthSm={4}
          dataWidthSm={8}
          groupWidthSm={12}
          onChange={(e)=>{e.preventDefault();}}
          help='help'
        />
        <h3>Input with name</h3>
        <FieldGroupEditWithKey
          key='key'
          value='value'
          valueType='value-type'
          name='name-field_group_edit_with_key'
          type='text'
          label='label'
          placeholder='placeholder'
          placeholderType='placeholder-type'
          onChange={(e)=>{e.preventDefault();}}
          onChangeType={(e)=>{e.preventDefault();}}
        />
        <h3>Static text field</h3>
        <FieldGroupText
          label='label'
          name='name'
          value='value'
          className=''
          labelClass=''
          textClass=''
          colLabel={4}
          colLabelOffset={0}
          colText={8}
        />
        <h3>Static text multiple field</h3>
        <FieldStaticMultiple
          name='name'
          label='label'
          value={[
            {"value":"value 1"},
            {"value":"value 2"},
            {"value":"value 3"}
          ]}
          colLabel={4}
          colText={8}
          colLabelOffset={0}
        />
        <h3>Simple select</h3>
        <SimpleSelect
          value='Num1'
          name='simple_select'
          label='label'
          placeholder='placeholder'
          list={[
            {"name": "Num1"},
            {"name": "Num2"},
            {"name": "Num3"}
          ]}
          fieldKey="name"
          fieldDisplay="name"
          labelWidthSm={4}
          dataWidthSm={8}
          onChange={(e)=>{e.preventDefault();}}
        />
        <h3>Switch checkbox</h3>
        <SwitchCheckbox
          label='label'
          value={true}
          onChange={(e)=>{e.preventDefault();}}
        />
      </PanelEdit.Form>
    </PanelEdit>
  );
}

export default compose(
  withProps(() => ({
    ui: {
      cancel: {
        en: 'Cancel',
        ru: 'Отмена',
      },
      saveChanges: {
        en: 'Save Changes',
        ru: 'Сохранить',
      },
      closeButton: {
        en: 'Close',
        ru: 'Закрыть',
      },
      title: {
        en: 'Sample form',
        ru: 'Пример формы',
      },
      multipleCheckbox: {
        Num1: {
          display: {
            en: 'Num1',
            ru: ''
          }
        },
        Num2: {
          display: {
            en: 'Num2',
            ru: ''
          }
        },
        Num3: {
          display: {
            en: 'Num3',
            ru: ''
          }
        },
      }
    },
  })),
)(PageAchEdit);

```

Let's look this sample form.

Section `import` defines external components, functions, styles. 
You must include React and Compose in every component. 
Use `WithProps` function of recompose to configure of UI (labels, titles and other text) with localization.
Use `import 'path/to/file_of_style.scss'` to add custom styles to component.

It's recommended to use react-bootstrap components instead of html with bootstrap classes, if it is possible. 
[](https://react-bootstrap.github.io/components.html "See the list of available components here.")
Example: 

`import {
  Button,
  Col,
  Form,
  FormControl,
  FormGroup,
  Row,
} from 'react-bootstrap';
`































