**## Zod Wrapper: Streamline Input Validation for Server and Client**

Tired of duplicating validation logic between your server and client code? Zod, the foundation of Zod Wrapper, is designed with developer experience in mind. It's a TypeScript-first library that allows you to define data structures, or schemas (encompassing everything from simple strings to intricate nested objects), using intuitive constructs. The key advantage? Automatic Type Inference. Declare a validator once, and Zod infers the corresponding TypeScript type, eliminating tedious type duplication and enhancing code readability. Furthermore, Zod excels at composing simpler types into complex data structures, making it well-suited for even the most demanding validation scenarios.

**Key Benefits:**

-   **Reduced Code Duplication:**  Define validation schemas once and share them between server and client, maintaining a single source of truth.
-   **Improved Maintainability:**  Easier to update validation rules in a single location, promoting code consistency and reducing the risk of errors.
-   **Enhanced Developer Experience:**  Focus on core application logic, leaving input validation to the dedicated Zod Wrapper package.
-   **Type-Safety:**  Leverage Zod's type-safe validation for better code readability and early error detection.

**Installation:**

Bash

```
npm install @ashu-bhai/common

```


**Usage:**

**1. Define Shared Validation Schemas:**

Create a file (e.g., `index.ts`) to house your Zod schemas accessible from both server and client code:

TypeScript

```
// validation-schemas.ts
import { z } from "zod";

export const signupInput = z.object({
  username: z.string().nonempty(),
  password: z.string().min(8).strong({
    // Use Zod's built-in strong password complexity checker or define custom rules
  }),
});

export  type  SignupParams  =  z.infer<typeof  signupInput>;

```



**2. Server-Side Validation:**

Import the shared schema from `validation-schemas` and use it to validate server-side input:

TypeScript

```
// server-side code (e.g., Node.js)
import { signupInput } from "@your-username/zod-wrapper";

const userData = { username: "john_doe", password: "password123" };

try {
  signupInput.parse(userData);
  console.log("Input validation successful!");
  // Proceed with processing validated data
} catch (error) {
  console.error("Input validation failed:", error.format());
  // Handle validation errors gracefully, e.g., return error response to client
}

```



**3. Client-Side Validation:**

Similarly, import the shared schema on the client-side and validate user input before sending it to the server:

TypeScript

```
// client-side code (e.g., React, Vue.js)
import { signupInput } from "@ashu-bhai/common";

const userData = { username: "ashutoh", password: "password2003" };

try {
  signupInput.parse(userData);
  console.log("Input validation successful!");
  // Send validated data to server
} catch (error) {
  console.error("Input validation failed:", error.format());
  // Display error messages to the user and prevent invalid submissions
}

```

**Contributing:**

We encourage contributions to the Zod Wrapper package! If you encounter issues, have suggestions, or want to implement new features, feel free to:

-   Open an issue on the project's GitHub repository (https://github.com/ashutoshgithubs/package-zod).
-   Submit a pull request with your contributions.

**Further Considerations:**

-   For complex validation rules, customize Zod's validation functions to match your specific requirements.
-   Consider implementing additional functionality within the Zod Wrapper package for improved error handling, data transformation, or integration with your chosen front-end framework.
