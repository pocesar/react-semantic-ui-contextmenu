# React Semantic-UI context menu
Thin wrapper for (context) menu using React Semantic-UI

## Usage

```jsx
import React from 'react'
import { ContextMenu } from 'react-semantic-ui-contextmenu'
import { Dropdown } from 'semantic-ui-react'

class MyContextMenuComponent extends React.Component {
  divRef = React.createRef()
  div2Ref = React.createRef()
  
  menuContent = ({ close, target }) => (
    <React.Fragment>
      {/* it's actually a Menu.Item with some ready-to-use functionality */}
      <ContextMenu.Item onClick={() => { doSomething().then(close) }}> 
        Open in new window
      </ContextMenu.Item>

      <ContextMenu.Item onClick={close}>
        Close menu
      </ContextMenu.Item>
      
      {this.div2Ref.current === target ? (
        <ContextMenu.Item>
          This only exists in "Also right click me"
        </ContextMenu.Item>
      ) : null}
      
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

  /* 
  takes an array of refs, multiple items can trigger the same context menu,
  but can trigger the open/close from outside using isOpen 
  */

  contextTargets = [this.divRef, this.div2Ref]
  
  onOpen = ({ target }) => {
    console.log('context menu opened', target)
  }
  
  onClose = () => {
    console.log('context menu closed')
  }
  
  render() {
    return (
      <div>
        <ContextMenu for={this.contextTargets} isOpen={false} onOpen={this.onOpen} onClose={this.onClose}>
          {this.menuContent}
        </ContextMenu>
        <div ref={this.divRef}>Right click me</div>
        <div ref={this.div2Ref}>Also right click me</div>
      </div>
    )
  }
}
```

## Why reusing Menu (and Menu.Item)?

The Semantic-UI Menu component makes it able to create complex, multi level menus without a major effort, making it really easy to create complex menus that are reusable and context-aware

## License 

MIT
