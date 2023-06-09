# IT314- Software Engineering  Lab-8
## Unit Testing and Continuous Integration (CI) using Github Actions

> * Take a module that you have implemented in any programming language. (Java, Python, C, C++, etc.)

Ans: <br> 
We have taken "Register" module for this task.

### Testing Frame Work Used: 
Jtest
```
npm install --save-dev jest
```

> * Write the test cases.<br>

user.test.js
```javascript
const { gql } = require("apollo-server-express");
const { describe } = require("node:test");

const { ApolloClient, InMemoryCache } = require("@apollo/client");

// intialize apollo client
const client = new ApolloClient({
  uri: "http://localhost:5000",
  cache: new InMemoryCache(),
});

// test suite
describe("Testing User CRUD", () => {
  it("Blank password is not allowed", async () => {
    const createUser = gql`
      mutation {
        register(
          registerInput: {
            username: "Anakin Skywalker"
            password: ""
            confirmPassword: ""
            email: "123@gmaiul.com"
          }
        ) {
          createdAt
          id
          email
          token
          username
        }
      }
    `;

    await expect(
      client.mutate({
        mutation: createUser,
      })
    ).rejects.toThrowError("Errors");
  });

  //test case 2 - email is not valid
  it("Email not valid", async () => {
    const createUser = gql`
      mutation {
        register(
          registerInput: {
            username: "A"
            password: "1234"
            confirmPassword: "1234"
            email: "dd123123.com"
          }
        ) {
          createdAt
          id
          email
          token
          username
        }
      }
    `;

    await expect(
      client.mutate({
        mutation: createUser,
      })
    ).rejects.toThrowError("Errors");
  }),
    //test case 3
    it("Should create a new user", async () => {
      const createUser = gql`
        mutation {
          register(
            registerInput: {
              username: "Anakin Skywalker"
              password: "123"
              confirmPassword: "123"
              email: "123@gmaiul.com"
            }
          ) {
            createdAt
            id
            email
            token
            username
          }
        }
      `;

      await expect(
        client.mutate({
          mutation: createUser,
        })
      ).rejects.toThrowError("Username is taken");
    });

  // test case 4
  it("Password not same", async () => {
    const createUser = gql`
      mutation {
        register(
          registerInput: {
            username: "Rick Sanchez"
            password: "1234"
            confirmPassword: "123"
            email: "12377777@gmaiul.com"
          }
        ) {
          createdAt
          id
          email
          token
          username
        }
      }
    `;

    await expect(
      client.mutate({
        mutation: createUser,
      })
    ).rejects.toThrowError("Errors");
  });

  //test case 5
  it("Should create a new user", async () => {
    const createUser = gql`
      mutation {
        register(
          registerInput: {
            username: "Anakin Skywalker"
            password: "123"
            confirmPassword: "123"
            email: "123@gmaiul.com"
          }
        ) {
          createdAt
          id
          email
          token
          username
        }
      }
    `;

    await expect(
      client.mutate({
        mutation: createUser,
      })
    ).rejects.toThrowError("Username is taken");
  });
});

// Referece :
// https://dev.to/neshaz/testing-graphql-server-in-nodejs-55cm
// https://blog.logrocket.com/writing-end-to-end-tests-for-graphql-servers-using-jest/
```

> * Execute the test cases by using the unit testing framework.
![image](https://user-images.githubusercontent.com/75716586/233694876-cb37eabc-494e-4ca7-9801-f66f0bd3815b.png)

> * Integrate your unit testing framework with GitHub.
![image](https://user-images.githubusercontent.com/75716586/233701606-40a6770e-8bfb-4bca-b0c5-3ee854ab9114.png)


> * Show all your works (test case passes, failed, execution time, and so on.)
![image](https://user-images.githubusercontent.com/75716586/233697112-48c75e63-be35-4c44-a29f-dd8a1a1d799e.png)

> * Once the test case is failed, How you fixed that?
To fix a failed test case in Node.js using Jtest, I first identify the cause of the failure by examining the error message provided. Then, I debug my code to find the root cause of the problem and make the necessary changes to fix the issue. Finally, I re-run the test case to ensure that it passes and repeat the process if necessary.
