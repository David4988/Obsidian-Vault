 [[Nextjs]]
  
- Nextjs uses **file system routing**, where **every folder** inside the `src` directory is a route.

```
   my-next-app/
	        ├── app/                     👈 Routing happens here (bye bye pages/)     
	        ├── route.tsx                 🏠 Home route (/)    
	        ├── layout.tsx               📐 Shared layout (header, footer, etc)/  
	        |── about/                   📁 Nested route    
	        |   └── route.tsx
	            └── contact/
	                └── route.tsx  
```
  
  
  
