### Redux Design Rules of Thumb: Questions to Ask

Here are **key questions** for deciding when to use slices, actions, selectors, and other Redux concepts, along with the corresponding decision points.

---

### **When to Use a Slice**

1. **Is the state specific to a feature or domain?**
   - **Yes:** Create a slice (e.g., `authSlice`, `productSlice`).
   - **No:** Consider using `useState` or `useReducer` locally.

2. **Does this state need to be shared across multiple components?**
   - **Yes:** Create a slice.
   - **No:** Use component-level state with `useState`.

3. **Will this state grow in complexity (e.g., more fields, actions)?**
   - **Yes:** Create a slice to prepare for scalability.
   - **No:** Keep it local or lightweight with `useState`.

4. **Does this state involve asynchronous actions like API calls?**
   - **Yes:** Create a slice and use `createAsyncThunk`.
   - **No:** A slice might not be necessary unless it’s global.

5. **Do you expect to reuse logic/actions across features?**
   - **Yes:** Create a slice to centralize the logic.
   - **No:** Consider simpler state management options.

---

### **When to Use Actions**

1. **Does the event describe a state change or user interaction?**
   - **Yes:** Create an action.
   - **No:** It might be handled by other middleware or local logic.

2. **Do multiple reducers need to respond to this event?**
   - **Yes:** Use an action to keep the event consistent across slices.

3. **Does the event require side effects (e.g., API calls)?**
   - **Yes:** Use `createAsyncThunk` to manage the async process.

4. **Is the action highly reusable across the app?**
   - **Yes:** Create a shared or global action.

---

### **When to Use Selectors**

1. **Is this state accessed in multiple components?**
   - **Yes:** Use a selector for consistency.
   - **No:** Directly access state with `useSelector`.

2. **Does the state require computed values or transformations?**
   - **Yes:** Use a selector to handle logic (e.g., calculating totals).

3. **Will the shape of the state change in the future?**
   - **Yes:** Use selectors to abstract state access and reduce refactoring.

4. **Is the state deeply nested?**
   - **Yes:** Use selectors to simplify component-level access.

---

### **When to Use Middleware (e.g., Thunks)**

1. **Does the logic involve asynchronous actions (e.g., API calls)?**
   - **Yes:** Use `createAsyncThunk` or middleware like Redux Thunk.

2. **Does the logic involve side effects (e.g., logging, analytics)?**
   - **Yes:** Use middleware to handle non-state-changing effects.

3. **Do you need to intercept and modify actions before they reach the reducer?**
   - **Yes:** Use middleware.

---

### **When to Use Local State (useState/useReducer)**

1. **Is the state only used in one or two components?**
   - **Yes:** Use `useState` or `useReducer`.

2. **Does the state change frequently within a single component?**
   - **Yes:** Use `useState` for simplicity.

3. **Does the state involve complex updates or logic?**
   - **Yes:** Use `useReducer` if confined to one component.

---

### **When to Use Global State (Redux)**

1. **Is the state shared across multiple components?**
   - **Yes:** Use Redux.

2. **Does the state need to persist across routes or sessions?**
   - **Yes:** Use Redux with storage mechanisms (e.g., Redux Persist).

3. **Does the state require centralized, predictable management?**
   - **Yes:** Use Redux to manage it systematically.

---

### **When to Use Reusable Utilities (e.g., Axios Instances)**

1. **Do you need consistent API handling across features?**
   - **Yes:** Create an Axios instance and share it across slices.

2. **Does the feature require common logic (e.g., error handling)?**
   - **Yes:** Use reusable utilities.

---

### Example Flow: Applying These Rules

- **Theme Settings**:  
  - Shared across multiple components → Create a `themeSlice`.
  - Access state in components → Use a selector like `selectTheme`.

- **Cart in an E-Commerce Site**:  
  - Requires global access → Create a `cartSlice`.
  - Needs API calls for fetching/updating → Use `createAsyncThunk`.
  - Total price requires calculation → Use a selector like `selectTotalPrice`.

- **Modal Visibility in a Component**:  
  - Used only in one component → Use `useState`.

- **Authentication**:  
  - Shared across the app (e.g., navbar, profile) → Create an `authSlice`.
  - Needs async login/logout logic → Use `createAsyncThunk`.

By asking these questions and following these rules, you can ensure your Redux system remains modular, scalable, and efficient.