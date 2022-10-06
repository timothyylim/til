### Adding Analytics to React App

#### To the component to track:
```javascript
import { Experiment, Variant, emitter } from '@marvelapp/react-ab-test';
import ReactGA from 'react-ga';

class Header extends React.Component {
  // Will register an event with the variantName in Events in Google Analytics
  sendEvent = (variantName: string) => {
    console.log('variant:', variantName)
    ReactGA.event({
      category: variantName,
      action: 'Clicked',
    });
  };

  render() {
    return (
      <Experiment ref="experiment" name="My Example">
        <Variant name="A">
          <div>
            <img src={`${process.env.REACT_APP_PUBLIC_ASSETS_URL}/images/minside_logo-desktop.svg`}
            className="header-logo"
            onClick={() => this.sendEvent("A")}
            />
          </div>            
        </Variant>
        <Variant name="B">
          <div>
            <img src="https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png"
            className="header-logo"
            onClick={() => this.sendEvent("B")}
            />
          </div>   
        </Variant>
      </Experiment>
    )
  }
};
```

#### To the main website
```javascript
import ReactGA from 'react-ga';
ReactGA.initialize('UA-144340339-1');
ReactGA.pageview(window.location.pathname + window.location.search);
```

### Other tips
* Has to be Class React.Component, and not a functional component 
* FireFox by default disables trackers. To confirm, you'll see this in the console log:
  ```
  Request to access cookie or storage on “https://www.google-analytics.com/collect?v=1&_v=j77&a=181386…4&tid=UA-144340339-1&_gid=1441659023.1563729848&z=1143710822” was blocked because it came from a tracker and content blocking is enabled.
  ```
  * Disable tracker blocking by clicking the shield/lock button on the left side of the address bar and then clicking "disable blocking for this site"
