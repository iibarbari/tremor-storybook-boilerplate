# Tremor-Storybook boilerplate 

### Initiate React Project
```bash
pnpm  create  vite
```

Select `React` ad framework
Select `JavaScript` as variant

### Add tailwind css
```bash
pnpm add -D tailwindcss
pnpm dlx tailwindcss init
```

### Initiate storybook
```bash
npx storybook@latest init
```

### Add tremor
```bash 
pnpm dlx @tremor/cli@latest init
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
	tags: ['autodocs'],  
	parameters: {  
		layout: 'fullscreen',  
	},  
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

If you run `pnpm run storybook` you should be able to see the `KPIProgressChart` component with necessary styling.

# Automate css export

```bash
pnpm add -D concurrently
```

