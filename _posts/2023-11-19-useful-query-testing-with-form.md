---
layout: post
title: Unit test with form
tags: [unit test, form, react]
# comments: true
---

<!-- Content here -->

## Some useful query for select element in form

1. Query input with name: `screen.getByRole("textbox", { name: /email/i })`
1. Submit form via button: `fireEvent.submit(screen.getByRole("button"))`
1. Add text value into input:

   ```js
   // Get by role => need aria-label="email" (same as name attribute) to use this query by name
   fireEvent.input(screen.getByRole("textbox", { name: /email/i }), {
     target: { value: "value inputted" },
   });

   // Get by label
   fireEvent.input(screen.getByLabelText("password"), {
     target: { value: "password" },
   });
   ```

## Mock some common library

1. Next Router

   ```js
   jest.mock("next/router", () => ({
     useRouter() {
       return {
         route: "/",
         pathname: "",
         query: "",
         asPath: "",
         push: jest.fn(),
         events: {
           on: jest.fn(),
           off: jest.fn(),
         },
         beforePopState: jest.fn(() => null),
         prefetch: jest.fn(() => null),
       };
     },
   }));
   const useRouter = jest.spyOn(require("next/router"), "useRouter");

   // Then in the tests
   useRouter.mockImplementation(() => ({
     route: "/",
     pathname: "",
     query: "",
     asPath: "",
     push: jest.fn(),
     events: {
       on: jest.fn(),
       off: jest.fn(),
     },
     beforePopState: jest.fn(() => null),
     prefetch: jest.fn(() => null),
   }));
   ```

## Setup mock global:

1. Create a file mock in the folder: <rootDir>/jest/**mocks**/routerMock.js
   ```js
   jest.mock("next/router", () => ({
     push: jest.fn(),
     back: jest.fn(),
     events: {
       on: jest.fn(),
       off: jest.fn(),
     },
     beforePopState: jest.fn(() => null),
     useRouter: () => ({
       push: jest.fn(),
     }),
   }));
   ```
1. Add jest setup in jest config
   ```js
   setupFilesAfterEnv: ['<rootDir>/jest.setup.js'],
   ```
1. Import mocks you want setup global
   ```js
   import "./jest/__mocks__/routerMock";
   ```

## Mock implementation

1.  Mock implementation a hook to return expected value

    ```js
    const mockFunction = jest.fn();

    jest.mock("next/navigation", () => ({
      usePathname: mockFunction,
    }));

    test("test case", () => {
      mockFunction.mockImplementation(() => "some-thing-returned");
    });
    ```

1.  Mock axios

    ```js
    import axios from 'axios';

    jest.mock("axios");

    test("good response", () => {
      axios.get.mockImplementation(() => Promise.resolve({ data: {...} }));
    });

    test("bad response", () => {
      axios.get.mockImplementation(() => Promise.reject({ ... }));
    })
    ```
