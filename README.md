# react-from-scratch
React 17, TypeScript + ESLint, WebPack+SCSS

## How to create project from scratch
1. Create directory and initialize project
```
	npm init -y
```

2. Create public director

3. Create index.html file in public directory
```html
    <html>
    <head>
        <meta charset="utf-8" />
        <title>React</title>
    </head>
    <body>
        <div id="root"></div>
    </body>
    </html>
```

4. Install React and TypeScript
```
	npm install react react-dom
	npm install --save-dev @types/react @types/react-dom typescript
```

5. Create src directory

6. Create index.tsx in src
```typescript
		import React from "react";
		import ReactDOM from "react-dom";
		import App from "./App";
		
		ReactDOM.render(
            <React.StrictMode>
            <App />
            </React.StrictMode>,
            document.getElementById("root")
		);
```
		
7. Create App component in src
```typescript
		import React from "react";
		import './styles.scss';
		
		const App: React.FC = () => {
		return (
		<div className="app-wraper">
		<h1>React 17 and TypeScript 4 App!🚀</h1>
		</div>
		  );
		};
		export default App;
```
		
		
8. Create tsconfig.json file in root directory
```json
		{
		  "compilerOptions": {
			"module": "commonjs",
			"moduleResolution": "node",
			"target": "ESNext",
			"removeComments": true,
			"allowSyntheticDefaultImports": true,
			"jsx": "react",
			"allowJs": true,
			"baseUrl": "src",
			"esModuleInterop": true,
			"resolveJsonModule": true,
			"downlevelIteration": true,
			"paths": {
			  "*": ["src/*"]
			},
			"lib": [
			  "esnext",
			  "dom",
			  "dom.iterable"
			],
			"sourceMap": true,
			"noImplicitAny": false,
		  },
		  "exclude": ["node_modules", "build"],
		  "include": [
			"./src",
			"webpack.config.ts" ]
		}
```		
		
9. Install eslint
```
	npm install --save-dev eslint  eslint-plugin-import eslint-plugin-react eslint-plugin-react-hooks  @typescript-eslint/eslint-plugin @typescript-eslint/parser
```


10. Install WebPack
```
	npm install --save-dev webpack webpack-cli webpack-dev-server ts-node @types/node @types/webpack @types/webpack-dev-server tsconfig-paths-webpack-plugin
	npm install --save-dev @types/webpack-dev-server
	npm install --save-dev html-webpack-plugin @types/html-webpack-plugin
	npm install --save-dev fork-ts-checker-webpack-plugin @types/fork-ts-checker-webpack-plugin
	npm install --save-dev ts-loader
	npm install --save-dev css-loader
	npm install --save-dev style-loader
```
	
11. Create webpack.config.ts in root directory
```typescript
	import path from "path";
	import { Configuration as WebpackConfiguration, DefinePlugin } from "webpack";
	import { Configuration as WebpackDevServerConfiguration } from "webpack-dev-server";
	import TsconfigPathsPlugin from 'tsconfig-paths-webpack-plugin';
	import ForkTsCheckerWebpackPlugin from "fork-ts-checker-webpack-plugin";
	import HtmlWebpackPlugin from "html-webpack-plugin";

	interface Configuration extends WebpackConfiguration {
		devServer?: WebpackDevServerConfiguration;
	  }

	const webpackConfig = (): Configuration => ({
	  entry: "./src/index.tsx",
	  ...(process.env.production || !process.env.development
		? {}
		: { devtool: "eval-source-map" }),

	  resolve: {
		extensions: [".ts", ".tsx", ".js"],
		plugins: [new TsconfigPathsPlugin({ configFile: "./tsconfig.json" })],
	  },
	  output: {
		path: path.join(__dirname, "/build"),
		filename: "build.js",
	  },
	  module: {
		rules: [
		  {
			test: /\.tsx?$/,
			loader: "ts-loader",
			options: {
			  transpileOnly: true,
			},
			exclude: /build/,
		  },
		  {
			test: /\.s?css$/,
			use: ["style-loader", "css-loader"],
		  },
		],
	  },
	  devServer: {
		port: 4200,
		open: true,
		historyApiFallback: true,
	  },
	  plugins: [
		new HtmlWebpackPlugin({
		  // HtmlWebpackPlugin simplifies creation of HTML files to serve your webpack bundles
		  template: "./public/index.html",
		}),
		// DefinePlugin allows you to create global constants which can be configured at compile time
		new DefinePlugin({
		  "process.env": process.env.production || !process.env.development,
		}),
		new ForkTsCheckerWebpackPlugin({
		  // Speeds up TypeScript type checking and ESLint linting (by moving each to a separate process)
		  eslint: {
			files: "./src/**/*.{ts,tsx,js,jsx}",
		  },
		}),
	  ],
	});

	export default webpackConfig;
```
	
12. Install node-sass
```
	npm install add node-sass
```
	
	
13. Create SCSS file in src/styles.scss
```scss
	.app-wraper {
		display: flex;
		justify-content: center;
		align-items: center;
	}
```
	
14. Create .eslintrc file in root directory
```json
{
    "parser": "@typescript-eslint/parser",
  
    "env": {
      "browser": true
    },
    "extends": [
      "plugin:@typescript-eslint/recommended",
      "plugin:react/recommended"
    ],
    "parserOptions": {
      "project": [
        "tsconfig.json"
      ],
      "ecmaVersion": 2020,
      "sourceType": "module",
      "ecmaFeatures": {
        "jsx": true
      }
    },
      "plugins": [
      "@typescript-eslint",
      "react",
      "react-hooks",
      "eslint-plugin-import"
    ],
    "rules": {
      "react-hooks/rules-of-hooks": "error",
      "react-hooks/exhaustive-deps": "warn",
      "@typescript-eslint/explicit-module-boundary-types": "off",
      "react/prop-types": "off"
    },
    "settings": {
      "react": {
        "version": "detect"
      }
    }
  }
```


15. Add scripts to package.json
```json
  "scripts": {
    "start": "webpack-cli serve --mode=development --env development --open --hot",
    "build": "webpack --mode=production --env production --progress",
    "lint": "eslint src/**/*.{ts,tsx} --quiet --fix"
  }
```

16. Start app
```
    npm start
```
