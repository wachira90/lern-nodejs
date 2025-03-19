The error **"Cannot use import statement outside a module"** happens because Node.js by default uses CommonJS, whereas `import` is an **ES module (ESM) syntax**.

### ✅ Fix 1: Use CommonJS (`require`)
Modify your script to use `require` instead of `import`:

```javascript
const { createClient } = require('redis');

const REDIS_HOST = '127.0.0.1';
const REDIS_PORT = 6379;
const REDIS_PASSWORD = 'your_redis_password';

const client = createClient({
    socket: {
        host: REDIS_HOST,
        port: REDIS_PORT
    },
    password: REDIS_PASSWORD
});

(async () => {
    try {
        await client.connect();
        console.log('Connected to Redis');

        const timestamp = Date.now();
        await client.set('tst', timestamp);
        console.log(`Saved timestamp: ${timestamp}`);

        const value = await client.get('tst');
        console.log(`Retrieved timestamp: ${value}`);

        await client.quit();
    } catch (err) {
        console.error('Redis error:', err);
    }
})();
```

---

### ✅ Fix 2: Enable ES Module Mode
If you prefer to use `import`, you need to **explicitly enable ES modules**.

#### Option 1: Rename file to `.mjs`
Rename your file to `app.mjs`, then run it with:

```sh
node app.mjs
```

#### Option 2: Update `package.json`
In your `package.json`, add:

```json
{
  "type": "module"
}
```

Then you can continue using `import`:

```javascript
import { createClient } from 'redis';
```

---

### 🛠️ Recommended Fix:
If you're working on an existing CommonJS-based project, **use Fix 1** (`require`).  
If you're starting fresh and prefer ES modules, **use Fix 2** (add `"type": "module"` or rename to `.mjs`).

Let me know if you need more help! 🚀
