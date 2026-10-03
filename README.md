# Pocket Ledger

A simple ledger for your money. Sign in with email, add payments, see monthly totals, a budget bar and charts, set up recurring payments, and import or export your data. Everything is stored in your own free Supabase database and is private to each account.

The whole app is one file, `index.html`. There is nothing to install or build.

## 1. Finish the database (once)

In Supabase, open **SQL Editor**, start a new query, paste the contents of `002_recurring_on_open.sql`, and press **Run**. It should say it succeeded. (You already ran `schema.sql`. Do not run that one again.)

This makes recurring payments post automatically when someone opens the app, and makes imports skip rows that are already saved.

## 2. Try it on your own computer

Double-click `index.html` to open it in your browser. Choose **Create account**, enter an email and a password of at least 8 characters, and sign up.

Supabase normally asks new users to confirm their email address. Its built-in email sending is limited, so for testing you may prefer to turn the confirmation off: in the dashboard open **Authentication**, find the **Email** sign-in provider, and switch off **Confirm email**. Turn it back on before real users arrive, and plan to connect a proper email sender then.

Then try: add a payment, edit it, delete it and tap Undo, add a recurring payment, import a CSV, and change the budget in Settings.

## 3. Put it online

1. Create a free account at github.com and a new repository named `pocket-ledger`.
2. In the repository choose **Add file**, then **Upload files**, and upload `index.html` and `README.md`. Commit.
3. Host it for free. Two easy options:
   - **GitHub Pages**: repository **Settings**, then **Pages**, then deploy from the `main` branch. Check GitHub's current rules on whether a private repository is allowed on the free plan. If not, make the repository public. That is safe: the publishable key in `index.html` is meant to be public, and the database rules keep each person's data private.
   - **Cloudflare Pages**: create a free Cloudflare account, choose **Workers and Pages**, connect your GitHub repository, and deploy with no build command.
4. Copy the web address you get, for example `https://yourname.github.io/pocket-ledger/`.
5. In Supabase open **Authentication**, then **URL Configuration**. Set the **Site URL** to your web address, and add the same address under **Redirect URLs**. Password reset and email confirmation links need this.

## 4. Keep the free project awake

On the free plan, Supabase pauses a project that gets no requests for 7 days. While you have few users, set up a free scheduled ping (for example a GitHub Actions workflow or a free uptime monitor) that opens your site's address once a day. Upgrading the plan removes the pause.

## Safety notes

- Never put the Supabase **secret** or **service_role** key in this file or anywhere in a browser. Only the publishable key belongs here.
- Row-level security is switched on for every table. A signed-in person can only read and change data in workspaces they belong to.
- Each account gets a personal workspace when it is created. Business workspaces with roles are already in the database design for the paid plan.
- Before real users: add a privacy page, turn email confirmation back on, and ask a lawyer or CA about data-protection and tax rules that apply to you.
