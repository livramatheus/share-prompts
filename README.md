# Promptopia

Promptoipia is an open-source AI prompting tool to discover, create and share creative prompts. Is a full-stack Next.js 13 application that I coded with the help of [Next.js 13 Full Course 2023](https://www.youtube.com/watch?v=wm5gMKuwSYk) as a way to keep me up to date with the latest Next.js features.

Below, you can see some key notes that I've taken during the course.

## General Notes

- To create a new project with the latest next features `npx create-next-app@latest ./`

## Next.js Back-end notes

- All endpoints should be placed under `app\api`. The url will match the folder structure automatically.

- `app\api\auth\[...nextauth]\route.js` - In this file, params related to authentication are set. Such as **Providers** (third-party auth vendors) and **Callbacks** (custom functions to be executed when a action is taken, such as `signIn` and `signOut`). In this case, the `signIn` callback function is used to create a new user into the database. This handler should be exported as `GET` and `POST`.

- Endpoints must be exported with the proper HTTP request type: `GET`, `POST`, `PATCH` and `DELETE`.

Example: `app\api\prompt\[id]\route.js`

```javascript
export const PATCH = async (request, { params }) => {
  const id = params.id;
  // ...
  return new Response(
    JSON.stringify(existingPrompt), { status: 200 }
  );
}
```

## Next.js Front-end notes

- Tailwind is now bundled with Next.js
- To set a component to be rendered on client side, it needs to be tagged with `use client` on the first line of the file.
- Tip! Whenever using states or hooks, it means that this component is a Client Side component.
- `useSearchParams` ("next/navigation") gets a read-only URLSearchParams object. For example `searchParams.get('foo')` would return 'bar' when `?foo=bar`):
- `head` elements can be set by exporting an object called `metadata` under `page.js`
- Base file structure: 

`app/layout.js` - app's main entry point. Anything you write in this file will be shared throughout the entired app.

`app/page.js` - is the page that we see when we access `localhost:3000`. `page.js` can be placed under folders to represent subfolders.


- `usePathname` ("next/navigation") hook gets the current pathname. For example `usePathname()` on /dashboard?foo=bar would return "/dashboard"
- Remember to involve session provider into the entire application.

```javascript
import { SessionProvider } from "next-auth/react";

const Provider = ({ children, session }) => {
  return (
    <SessionProvider session={session}>
      {children}
    </SessionProvider>
  )
}

export default Provider;
```