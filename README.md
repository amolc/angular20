# angular20



## Part 1: Angular Frontend Setup (my-angular-app)

### 1. Project Initialization
- **Create Project**: `ng new admin-app`
- **Options**: Select `Yes` for routing and choose your preferred stylesheet format (e.g., CSS).
- **Structure**: This project uses **Standalone Components**, which is the modern standard for Angular 19+.

### 2. Component Generation
Generated two main components using Angular CLI:
- `ng generate component login --skip-tests`: For the authentication interface.
- `ng generate component users --skip-tests`: For user listing and management.

### 3. Service Creation (`src/app/auth.service.ts`)
The `AuthService` is the heart of the application's data logic.
- **`login(email, password)`**: Sends a POST request to the Django login endpoint and stores the user in `localStorage` upon success.
- **`getUsers()`**: Fetches the list of all users from the API.
- **`addUser(user)`**: Sends a POST request to create a new user record.
- **`isLoggedIn()`**: Checks if a user is currently stored in local storage.

### 4. Application Configuration (`src/app/app.config.ts`)
- **`provideHttpClient()`**: Essential for allowing Angular to make HTTP requests to the backend API.
- **`provideRouter(routes)`**: Enables navigation between different parts of the app.

### 5. Routing Configuration (`src/app/app.routes.ts`)
Defined paths for the application:
- `/login`: Points to the `LoginComponent`.
- `/users`: Points to the `UsersComponent`.
- Empty path (`''`): Redirects to `/login`.

### 6. Component Breakdown

#### LoginComponent (`src/app/login/`)
- **`login.component.ts`**: Handles the form submission logic. It calls the `AuthService.login()` method and navigates to the `/users` page if successful.
- **`login.component.html`**: A clean UI with a form for Email and Password inputs, using `[(ngModel)]` for two-way data binding.

#### UsersComponent (`src/app/users/`)
- **`users.component.ts`**: 
    - On initialization (`ngOnInit`), it checks if the user is logged in.
    - Manages the state for the user list and the "Add User" form.
    - Implements `loadUsers()` to refresh the list from the backend.
- **`users.component.html`**: 
    - Displays a table of users using the `*ngFor` structural directive.
    - Contains a toggleable form to add new users to the database.

### 7. Main Entry Point (`src/app/app.component.html`)
Replaced the default boilerplate with `<router-outlet></router-outlet>`, which acts as a placeholder that Angular dynamically fills based on the current URL.
