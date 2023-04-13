# react_101

Setting Up a React Project Without Create React App

While Create React App (CRA) provides a quick and easy way to set up a React project, it may not be suitable for all use cases. In this article, we will walk you through setting up a React project from scratch without CRA, covering topics like project structure, Webpack configuration, Babel setup, and installing essential React dependencies.

0. Prerequisites
Ensure you have Node.js and npm installed on your computer. You can check their installation by running the following commands:

node -v
npm -v
1. Project Setup
First, we create a new directory for the project and navigate to it in the terminal. This step creates a folder where all our project files will be located.

mkdir react-app
cd react-app
We then initialize a new package.json file, which will store the project's metadata and dependencies.

npm init -y
2. Installing React and ReactDOM
Next, we install the core React libraries: react and react-dom. These libraries are essential for creating React components and rendering them in the browser.

npm install react react-dom
3. Babel Setup
Babel is a JavaScript compiler that allows you to use the latest JavaScript features while maintaining support for older browsers. This step ensures your code is compatible with a wide range of browsers.

Make sure to install them in devDependencies. Placing development-related libraries in the devDependencies section is a best practice because it helps distinguish between the dependencies required for the application to run and those needed only during development.

Install the necessary Babel dependencies in devDependencies:

npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader
Create a .babelrc configuration file in your project's root directory. This file tells Babel which presets to use when transpiling your code.

{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
4. Webpack Configuration
Webpack is a module bundler that processes and bundles your application’s assets, such as JavaScript, CSS, and images. It takes your source files and creates a single, optimized output file for the browser.

Install the required Webpack dependencies in devDependencies:

npm install --save-dev webpack webpack-cli webpack-dev-server html-webpack-plugin css-loader style-loader
Create a webpack.config.js file in your project's root directory. This configuration file tells Webpack how to process and bundle your project files.

mode: Sets the mode for the build process (development or production).
entry: Specifies the entry point for your application.
output: Defines where the bundled files will be saved.
module.rules: Determines how different file types should be processed.
resolve.extensions: Specifies which file extensions Webpack should resolve.
plugins: Configures additional plugins, such as the HtmlWebpackPlugin.
devServer: Sets up the development server configuration.
const HtmlWebpackPlugin = require('html-webpack-plugin');
const path = require('path');

module.exports = {
  mode: 'development',
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader',
        },
      },
      {
        test: /\.css$/,
        use: ['style-loader', 'css-loader'],
      },
    ],
  },
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './public/index.html',
    }),
  ],
  devServer: {
    static: {
      directory: path.join(__dirname, 'dist'),
    },
    hot: true,
    open: true,
  },
};
5. Project Structure
Create a basic project structure:

my-custom-react-app/
  ├── public/
      ├── index.html
  ├── src/
      ├── App.js
      ├── index.js
  ├── .babelrc
  ├── package.json
  ├── webpack.config.js
Create a simple index.html file inside the public folder. This file serves as the main HTML template for your application, and it’s where the React components will be rendered.

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My Custom React App</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
Create an index.js file inside the src folder. This file is the entry point of your application and is responsible for rendering the root React component.

import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
Create an App.js file inside the src folder. This file defines the main App component, which can be used to build the rest of your application.

import React from 'react';

const App = () => {
  return <div>Hello, world!</div>;
};
export default App;
6. Running the Application
Add the following scripts to your package.json file. These scripts allow you to run your application in development mode or create a production build.

"scripts": {
  "start": "webpack serve --mode development",
  "build": "webpack --mode production"
}
Now you can run your custom React application in development mode:

npm start
This command will open a new browser window with your application running at http://localhost:8080/.

7. Set up .gitignore
Before pushing up to the GitHub repository, create a .gitignore file in the root of your project directory and include the following:

# .gitignore

# Ignore node_modules folder
node_modules/

# Ignore environment variables and secrets
.env

# Ignore build folder
/dist
/build

# Ignore logs
*.log
This .gitignore file will ensure that the node_modules folder, the .env file containing environment variables or secrets, and the build folder are not pushed to the remote repository.

8. Optional: Adding CSS Preprocessors
If you prefer to use a CSS preprocessor like SCSS, you can install the necessary dependencies and adjust the Webpack configuration:

Install SCSS dependencies in devDependencies:

npm install --save-dev sass-loader sass
Update the Webpack configuration by modifying the rules array:

{
  test: /\.scss$/,
  use: ['style-loader', 'css-loader', 'sass-loader'],
}
Now you can use SCSS files in your project.

GitHub - claudeando/react_101
You can't perform that action at this time. You signed in with another tab or window. You signed out in another tab or…
github.com

You now have a custom React application set up without using Create React App. This configuration provides more flexibility and allows you to customize the build process to fit your specific needs. It’s an excellent starting point for projects requiring a more tailored setup or for developers looking to learn more about the underlying build tools. This beginner-friendly guide should have provided you with the explanations needed to understand the purpose and importance of each step in the process.

React
Cra
