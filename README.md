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