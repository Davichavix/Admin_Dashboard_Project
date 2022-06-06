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

//Sidebar.jsx

import { useStateContext } from '../contexts/ContextProvider';

const Sidebar = () => {
  const{ activeMenu, setActiveMenu } = useStateContext();

```