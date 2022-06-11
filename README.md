# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

### David's Notes

1. utilize ternary operator to render compoenents given true variable
```
          {activeMenu ? (
            <div>
              Sidebar
            </div>
          ) : (
            <div>
              Sidebar w-0
            </div>
          )}
```

2. utilize template literals and ternary operators to reduce repeat code when using conditional className

```
          <div className={ 
            `dark:bg-main-bg bg-main-bg min-h-screen w-full ${activeMenu} ? 'md:ml-72 : flex-2`
          }>
```

3. use React Routes, Route from react-router-dom to add multipage links/routes

```

          <div>
            <Routes>
              {/* Dashboard */}
              <Route path="/" element="Ecommerce"/>
              <Route path="/ecommerce" element="Ecommerce"/>
              {/* Pages */}
              <Route path="/orders" element="Orders"/>
              <Route path="/employees" element="Employees"/>
              <Route path="/customers" element="Customers"/>

              {/* Apps */}
              <Route path="/kanban" element="Kanban"/>
              <Route path="/editor" element="Editor"/>
              <Route path="/calendar" element="Calender"/>
              <Route path="/color-picker" element="ColorPicker"/>
            </Routes>
          </div>

```

4. Use an index.jsx component to allow the import of all components in one line

```
//index.jsx

export { default as Button } from './Button';
export { default as ThemeSettings } from './ThemeSettings';
export { default as Sidebar } from './Sidebar';
export { default as Navbar } from './Navbar';
export { default as Footer } from './Footer';
export { default as Cart } from './Cart';
export { default as Chat } from './Chat';
export { default as Notification } from './Notification';
export { default as UserProfile } from './UserProfile';
export { default as SparkLine } from './Charts/SparkLine';
export { default as LineChart } from './Charts/LineChart';
export { default as Stacked } from './Charts/Stacked';
export { default as Pie } from './Charts/Pie';
export { default as ChartsHeader } from './ChartsHeader';
export { default as Header } from './Header';

```

5. Use pre-build react icons by importing
```
import { SiShopware } from 'react-icons/si'

```

6. Map over array of items in components for more succinct code.
```
        <div className="mt-10">
          {links.map((item) => (
            <div className="text-gray-400 m-3 mt-4 uppercase">
              {item.title}
            </div>
          ))}
        </div>
```

7. Save links in array of objects allowing easy access to rendering link and titles for sidebar
```
export const links = [
  {
    title: 'Dashboard',
    links: [
      {
        name: 'ecommerce',
        icon: <FiShoppingBag />,
      },
    ],
  },

  {
    title: 'Pages',
    links: [
      {
        name: 'orders',
        icon: <AiOutlineShoppingCart />,
      },
      {
        name: 'employees',
        icon: <IoMdContacts />,
      },
      {
        name: 'customers',
        icon: <RiContactsLine />,
      },
    ],
  },
  {
    title: 'Apps',
    links: [
      {
        name: 'calendar',
        icon: <AiOutlineCalendar />,
      },
      {
        name: 'kanban',
        icon: <BsKanban />,
      },
      {
        name: 'editor',
        icon: <FiEdit />,
      },
      {
        name: 'color-picker',
        icon: <BiColorFill />,
      },
    ],
  },
  {
    title: 'Charts',
    links: [
      {
        name: 'line',
        icon: <AiOutlineStock />,
      },
      {
        name: 'area',
        icon: <AiOutlineAreaChart />,
      },

      {
        name: 'bar',
        icon: <AiOutlineBarChart />,
      },
      {
        name: 'pie',
        icon: <FiPieChart />,
      },
      {
        name: 'financial',
        icon: <RiStockLine />,
      },
      {
        name: 'color-mapping',
        icon: <BsBarChart />,
      },
      {
        name: 'pyramid',
        icon: <GiLouvrePyramid />,
      },
      {
        name: 'stacked',
        icon: <AiOutlineBarChart />,
      },
    ],
  },
];

```

8. Store multiple initial states in single stateobject 
 - State should be held by the highest parent component in the stack that requires access to the state

```
const initialState = {
  chat: false,
  cart: false,
  userProfile: false,
  notification: false,
}

```

9. Using context, we can avoid passing props through intermediate elements
 -  Provider component accepts a value prop to be passed to consuming components that are descendants of this Provider
 - All consumers that are descendants of a Provider will re-render whenever the Provider’s value prop changes
 - When to use context:
    - global state
    - theme
    - application configuration
    - authenticated user name
    - user settings
    - preferred language
    - a collection of services

```
//ContextProvider.js

import React, { createContext, useContext, useState } from 'react';

const StateContext = createContext();

const initialState = {
  chat: false,
  cart: false,
  userProfile: false,
  notification: false,
}

export const ContextProvider = ({ children }) => {
  const [activeMenu, setActiveMenu] = useState(true);

  return (
    <StateContext.Provider
      value={{
        activeMenu,
        setActiveMenu,
      }}
    >
      {children}
    </StateContext.Provider>
    )
}

export const useStateContext = () => useContext(StateContext);

```
```
//index.js (Entire App must be wrapped in context provider)

import { ContextProvider } from './contexts/ContextProvider';

ReactDOM.render(
  <ContextProvider>
      <App />
  </ContextProvider>,
  document.getElementById('root'),
);

```
```
//App.js (Required to import useStateContext to each component allowing access to activeMenu value)

import { useStateContext } from './contexts/ContextProvider';

const App = () => {
  const { activeMenu } = useStateContext()
  ...

```
```
//Sidebar.jsx

import { useStateContext } from '../contexts/ContextProvider';

const Sidebar = () => {
  const{ activeMenu, setActiveMenu } = useStateContext();

```

10. Create Button components that take custom props to allow for unique functionality while maintaining reusability
- customFunc is function that is customizable
- icon is custom icon
- color is custom color

```
const NavButton = ({title, customFunc, icon, color , dotColor}) => (
  <TooltipComponent content={title}
  position="BottomCener">
    <button type="button" 
    onClick={customFunc} 
    style={{ color }}
    className="relative text-xl rounded-full p-3 hover:bg-light-gray"
    >
      <span style={{background: dotColor}}
      className="absolute inline-flex rounded-full h-2 w-2 right-2 top-2"
      >
        {icon}
      </span>
    </button>
  </TooltipComponent>
)

```
```
Below the NavButton componenet has custom props passed to it

const Navbar = () => {
  const { activeMenu, setActiveMenu } = useStateContext();
  return (
    <div className = "flex justify-between p-2 md:mx-6 relative">
      <NavButton title="Menu" customFunc={() => setActiveMenu((prevActiveMenu) => 
        !prevActiveMenu)} 
        color="blue" 
        icon={<AiOutlineMenu /> }
        />
    </div>
  )
}
```

11. when state is an object - subsequent state values can be accessed as keys 

```
const initialState = {
  chat: false,
  cart: false,
  userProfile: false,
  notification: false,

```
```
{isClicked.cart && <Cart />}
{isClicked.chat && <Chat />}
{isClicked.notification && <Notification />}
{isClicked.userProfile && <UserProfile />}

```

12. Use spread operator to update object value for cleaner code
  

```
setClicked("cart") will change isClicked.cart => true

```

```
const initialState = {
  chat: false,
  cart: false,
  userProfile: false,
  notification: false,
}

export const ContextProvider = ({ children }) => {
  const [activeMenu, setActiveMenu] = useState(true);
  const [isClicked, setIsClicked] = useState(initialState);


// handleClick function changes initialState key to true
  const handleClick = (clicked) => {
    setIsClicked({...initialState, [clicked]: true});
  }

```

13. Combination of state and useEffect can be used to setScreensize for responsive design
- Sidebar hides if screensize width is smaller than 900px

  1. useState is used to set initial screen size to undefined
  2. useEffect upon refresh adds the "resize" event listener to the window
  3. A handleResize function is called that sets screenSize to the initial innerWidth of the window
  4. immediately after the resize event listener is removed from window (removeEventListener should contain both the type 'resize' and listener function 'handleResize)
  5. Second useEffect is used to to call setActiveMenu(true || false) upon changes in the screenSize state
  6. Additional UI improvements include closing the side bar upon clicking link in Sidebar (For mobile application only)

```
  const [screenSize, setScreenSize] = useState(undefined);

```

```
  useEffect(() => {
    const handleResize = () => setScreenSize(window.innerWidth);

    window.addEventListener('resize', handleResize);

    handleResize();

    return () => window.removeEventListener('resize', handleResize);
  }, []);

  ```

  ```
    useEffect(() => {
    if(screenSize <= 900) {
      setActiveMenu(false);
    } else {
      setActiveMenu(true);
    }
  }, [screenSize]);

  ```

  14. Template for reusable react button (Pass styles as props to button component allows for reusable code)
    1. bgColor - background color
    2. color - font color
    3. button size
    4. name of the button

  ```
              <Button 
              color="white"
              bgColor="blue"
              text="Download"
              borderRadius="10px"
              size="md"
            />
  ```
  ```
    //Button.jsx
  const Button = ({ bgColor, color, size, text, borderRadius}) => {
    return (
      <button 
        type="button"
        style={{backgroundColor: bgColor, color, borderRadius}}
        className={`text-${size} p-3 hover:drop-shadow-xl`}
      >
        {text}
      </button>
    )
  }
  ```