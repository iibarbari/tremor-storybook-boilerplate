# Setup Tremor-Storybook Repo

### Initiate React Project
```bash
npm create vite
```

Select `React` ad framework
Select `JavaScript` as variant

### Add tailwind css
```bash
npm add -D tailwindcss
npx tailwindcss init
```

### Initiate storybook
*Notes*
Your node version should be 16 and below.
```bash
nvm install 16
nvm use 16
```

1. Download necessary packages
```bash
npm i -D @storybook/addon-actions@6.5.16 @storybook/addon-essentials@6.5.16 @storybook/addon-links@6.5.16 @storybook/react@6.5.16 @storybook/builder-webpack5@6.5.16 @storybook/manager-webpack5@6.5.16 webpack@^5
```
2. Add storybook commands to `package.json`
```json
"scripts": {
	"storybook": "start-storybook -p 6006",  
	"build-storybook": "build-storybook"  
},
```
3. Remove this line from the `package.json`
```bash
"type": "module",
```

4. Create `.storybook` folder
```bash 
mkdir .storybook
touch .storybook/main.js .storybook/preview.js
```
5. Paste the code below to `.storybook/main.js` file
```js 
module.exports = {  
	"core": {  
		"builder": "webpack5",  
	},
	"stories": [  
		"../src/**/*.stories.mdx",  
		"../src/**/*.stories.@(js|jsx|ts|tsx)"  
	],  
	"addons": [  
		"@storybook/addon-links",  
		"@storybook/addon-essentials"  
	]  
}
```
6. Paste the code below to `.storybook/preview.js` file
```js
export const parameters = {  
	actions: { argTypesRegex: "^on[A-Z].*" },  
	controls: {  
		matchers: {  
			color: /(background|color)$/i,  
			date: /Date$/,  
		},  
	},  
}
```
7. Test if it work, if succesful go to next step.
```bash 
npm run storybook
```


### Add tremor
```bash 
npx @tremor/cli@latest init
```

- Select `Vite`  as framework

### Add your first tremor component
```bash 
mkdir src/components
mkdir src/components/KPIProgressChart
touch src/components/KPIProgressChart/index.jsx src/components/KPIProgressChart/KPIProgressChart.stories.js 
```

- Paste this component to  `index.jsx` file

```jsx 
import {Card, Text, Metric, Flex, ProgressBar} from "@tremor/react";  
  
export default function KPIProgressChart() {  
	return (  
		<Card className="max-w-xs mx-auto">  
			<Text>Sales</Text>  
			<Metric>$ 71,465</Metric>  
			<Flex className="mt-4">  
				<Text>32% of annual target</Text>  
				<Text>$ 225,000</Text>  
			</Flex>  
			<ProgressBar value={32} className="mt-2" />  
		</Card>  
	)  
}
```

- Paste the story below to the `KPIProgressChart.stories.js` file.

```js
import {default as KPIProgressChart} from './index.jsx';
  
export default {  
	title: 'Components/KPIProgressChart',  
	component: KPIProgressChart, 
};  
  
export const Default = {  
	args: {},  
};
```

### Export tailwind.css

```bash 
npx tailwindcss -o src/styles/tailwind.css --minify
```

- You should be seeing `tailwind.css` file under `src/styles`.
- Consume this CSS file from `.storbook/preview.js`  by adding the import below.
```js 
import '../src/styles/tailwind.css';
```

If you run `npm run storybook` you should be able to see the `KPIProgressChart` component with necessary styling.
