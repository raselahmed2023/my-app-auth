

# 📝 Better Auth & MongoDB Installation Steps

### Step 1: Install the Package
Open your terminal and run:
```bash
npm install better-auth
```

### Step 2: Set Environment Variables
1. Visit the Better Auth website to generate your auth secret.
2. Create a `.env` file in your root directory.
3. Add your base URL and the secret.

```env
BETTER_AUTH_SECRET=your_generated_code_here
BETTER_AUTH_URL=http://localhost:3000
```

### Step 3: Create A Better Auth Instance
Create a file at `app/lib/auth.js` (or `.ts`) to initialize the library.

### Step 4: Install MongoDB Adapter
Run the following command to install MongoDB support:
```bash
npm install @better-auth/mongo-adapter mongodb
```

### Step 5: Configure `auth.js`
Paste the following code into your `app/lib/auth.js` file to connect Better Auth with your MongoDB database:

```javascript
import { betterAuth } from "better-auth";
import { MongoClient } from "mongodb";
import { mongodbAdapter } from "better-auth/adapters/mongodb";

// Replace with your MongoDB connection string
const client = new MongoClient("mongodb://localhost:27017/database");
const db = client.db();

export const auth = betterAuth({
  database: mongodbAdapter(db, {
    // Providing the client enables database transactions
    client 
  }),
});
```

### Step 6: Connect MongoDB Atlas
Visit [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) to set up your cloud database. Use the connection hook/string in your `.env` or `auth.js` file for production.

### Step 7: Authentication Methods
Configure the methods you want to use. Better Auth supports email/password and social logins out of the box. Update your `auth.ts` / `auth.js` like this:

```javascript
import { betterAuth } from "better-auth";

export const auth = betterAuth({
  // ... (previous database config)
  emailAndPassword: { 
    enabled: true, 
  },
});
```

---

