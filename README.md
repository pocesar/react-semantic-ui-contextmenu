# React Semantic-UI context menu
Thin wrapper for (context) menu using React Semantic-UI

## Usage

```jsx
import React from 'react'
import { ContextMenu } from 'react-semantic-ui-contextmenu'
import { Dropdown } from 'semantic-ui-react'

class MyContextMenuComponent extends React.Component {
  menuContent = ({ close }) => (
    <React.Fragment>
      {/* it's actually a Menu.Item with some ready-to-use functionality */}
      <ContextMenu.Item onClick={() => { doSomething().then(close) }}> 
        Open in new window
      </ContextMenu.Item>

      <ContextMenu.Item onClick={close}>
        Close menu
      </ContextMenu.Item>
      
      {/* behaves exactly like https://react.semantic-ui.com/collections/menu/#content-sub-menu */}
      <Dropdown item text='More'> 
        <Dropdown.Menu>
          <Dropdown.Item icon='edit' text='Edit Profile' />
          <Dropdown.Item icon='globe' text='Choose Language' />
          <Dropdown.Item icon='settings' text='Account Settings' />
        </Dropdown.Menu>
      </Dropdown>
    </React.Fragment>
  )
  
  render() {
    return (
      <div>
        <ContextMenu for={[ this.divRef ]}>
          {this.menuContent}
        </ContextMenu>
        <div ref={(_ref) => (this.divRef = _ref)}>Right click me</div>
        {/* this could also be created using React.createRef() */}
      </div>
    )
  }
}
```

## Why reusing Menu (and Menu.Item)?

The Semantic-UI Menu component makes it able to create complex, multi level menus without a major effort, making it really easy to create complex menus that are reusable and context-aware

## License 

MIT
