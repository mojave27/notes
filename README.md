# notes

## theming

**App.js**
```javascript
import { Fragment, useEffect, useState } from 'react'
import * as React from 'react'
import { MuiThemeProvider } from '@material-ui/core/styles'
import { createMuiTheme } from '@material-ui/core/styles'
// eslint-disable-next-line no-unused-vars
import { lightTheme, darkTheme } from './styles/Themes'
import CssBaseline from '@material-ui/core/CssBaseline';
import Main from './components/Main'
import Cookies from 'universal-cookie';


function App() {
  const [theme, setTheme] = useState(true)
  const currentTheme = createMuiTheme(theme ? darkTheme : lightTheme)

  useEffect(() => {
    const getUserTheme = () => {
      const cookies = new Cookies()
      let themeValue = 'true' === cookies.get('metrics-theme')
      setTheme(themeValue)
    }
    getUserTheme()
  }, [])

  const toggleTheme = () => {
    const cookies = new Cookies()
    cookies.set('metrics-theme', !theme, { path: '/' })
    setTheme(!theme)
  }

  return (
    <Fragment>
      <MuiThemeProvider theme={currentTheme} >
        <CssBaseline />
        <Main toggleTheme={toggleTheme} />
      </MuiThemeProvider>
    </Fragment>
  );
}

export default App;
```

**DarkTheme**
```javascript
import { createMuiTheme } from '@material-ui/core/styles'

export const darkTheme = createMuiTheme({
    palette: {
      type: "dark",
      primary: {
        main: "#222"
      }
    }
});
```
