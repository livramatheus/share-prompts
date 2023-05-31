## Promptopia

Promptoipia is an open-source AI prompting tool to discover, create and share creative prompts. Is a full-stack Next.js 13 application that I coded with the help of [Next.js 13 Full Course 2023](https://www.youtube.com/watch?v=wm5gMKuwSYk) as a way to keep me up to date with the latest Next.js features.

Below, you can see some key notes that I've taken during the course.

### Next.js Back-end notes

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