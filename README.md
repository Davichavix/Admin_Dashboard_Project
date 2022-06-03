# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

### Notes

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

2. utilize template literals and ternary operators to reduce repeat code when using conditioanl className

```
          <div className={ 
            `dark:bg-main-bg bg-main-bg min-h-screen w-full ${activeMenu} ? 'md:ml-72 : flex-2`
          }>
```