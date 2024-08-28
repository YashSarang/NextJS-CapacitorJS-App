# NextJS-CapacitorJS-App/Boilerplate template
Open in Code Editor for copying code

## Step 1: Setting Up a Next.js Project

1. Create a New Next.js App:
Use create-next-app to set up a new Next.js project.
```
npx create-next-app@latest
*What is your project named? » my-app*
*Would you like to use TypeScript? » Yes*
*Would you like to use ESLint? ... Yes*
*Would you like to use Tailwind CSS? ... Yes*
*Would you like to use `src/` directory? ... Yes*
*Would you like to use App Router? (recommended) ... Yes*
*Would you like to customize the default import alias (@/*)? ... Yes*
*What import alias would you like configured? » @/*/*
```
2. Setting Up the @ Alias, Configure jsconfig.json or tsconfig.json:\
Add the following configuration to your jsconfig.json (or tsconfig.json for TypeScript):
```
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```
3. Update Next.js Configuration:
In your next.config.js, you can ensure that the alias works with Next.js by adding:
```
/** @type {import('next').NextConfig} */
import * as path from 'path';
import { fileURLToPath } from 'url';
import { dirname } from 'path';

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);
const nextConfig = {
    webpack: (config) => {
    config.resolve.alias['@'] = path.resolve(__dirname, 'src');
    return config;
  },
  output: "export",
  distDir: 'out',
  images: {
    unoptimized: true, // For static export
  },
};
export default nextConfig;
```

## Step 2: Set Up Capacitor
1. Install capacitor 
```
npm install @capacitor/core @capacitor/cli   
npx cap init                                 
*Name ... App*                               
*Package ID ... com.example.app*                
```
```
npm install @capacitor/ios @capacitor/android
```
2. Ensure index.html Exists
Check the public Directory:                  
>Make sure that your Next.js project has an index.html file in the public directory. However, Next.js doesn’t use index.html directly; it uses the pages directory.

Create an index.html File:                       
>You need to create an index.html file manually if it doesn’t exist. Place it in the public directory. For Next.js, this file can be minimal since the main content is served by Next.js pages.

Create a folder in the root(my-app) directory named "out" \
Create a file named index.html in the out directory with basic HTML content: 
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>My Next.js App</title>
  </head>
  <body>
    <div id="__next"></div>
  </body>
</html>
```

Edit capacitor.config.ts or capacitor.config.json:
Make sure the webDir property points to the directory where your static files are located:
```
{
  "appId": "com.example.app",
  "appName": "App",
  "webDir": "out",
  "server": {
    "androidScheme": "https"
  }
}
```
```
npx cap add android                 
npx cap add ios                     
npx cap copy                        
```
3. Run the Development Server:

Start the development server to see your app in action.\
```
npm run dev     
```
Your app will be available at http://localhost:3000.   \
