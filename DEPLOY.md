# Deploy Green Quest to Render (Free, Shareable Link)

Follow these steps to get a **permanent shareable link** for your Green Quest app.

## 1. Push to GitHub

Ensure your project is in a GitHub repository:

```bash
git add .
git commit -m "Prepare for deployment"
git push origin main
```

## 2. Deploy on Render

1. Go to **[render.com](https://render.com)** and sign up (free).

2. Click **New +** → **Blueprint**.

3. Connect your GitHub account and select the `green-quest` repository.

4. Render will detect `render.yaml` and create:
   - A **Web Service** for the app
   - A **PostgreSQL** database

5. Click **Apply** to deploy.

6. Wait for the build to finish (about 5–10 minutes the first time).

## 3. Your Shareable Link

When the deploy finishes, your app will be available at:

```
https://green-quest-XXXX.onrender.com
```

This URL is **shareable** with anyone. Free tier notes:
- App sleeps after 15 minutes of inactivity (first load can take 30–60 seconds)
- Database and app are hosted on Render’s free tier

## 4. Seed the Database (Optional)

To create the admin user and sample quests, use Render’s **Shell**:

1. In your Render dashboard, open the **green-quest** service.
2. Go to **Shell**.
3. Run:
   ```bash
   cd server && npx prisma db seed
   ```
4. Admin account: **admin@greenquest.com** / **admin123**

## Alternative: Deploy Without Blueprint

If you deploy manually (without Blueprint):

1. Create a **PostgreSQL** database on Render.
2. Create a **Web Service** connected to your repo.
3. Set:
   - **Build Command**: `npm install && cd client && npm install && npm run build && cd ../server && npm install && npm run build`
   - **Start Command**: `npm start`
   - **Release Command**: `cd server && npx prisma migrate deploy`
4. Add environment variables:
   - `DATABASE_URL` (from the PostgreSQL service)
   - `JWT_SECRET` (any random long string)
   - `NODE_ENV` = `production`
