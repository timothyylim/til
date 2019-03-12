# react

Listen for clicks outside an element. E.g. menus

```
import ReactDOM from 'react-dom';

componentDidMount() {
    document.addEventListener('click', this.handleClickOutside, true);
}

componentWillUnmount() {
    document.removeEventListener('click', this.handleClickOutside, true);
}

handleClickOutside = event => {
    const domNode = ReactDOM.findDOMNode(this);

    if (!domNode || !domNode.contains(event.target)) {
        this.setState({
            visible: false
        });
    }
}
```

You can also use hooks. [Read more](https://stackoverflow.com/questions/32553158/detect-click-outside-react-component/42234988#42234988)
