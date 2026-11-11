# 3D Smart Warehouse

Files:
- `index.html` : the whole app (already has the Supabase settings)
- `supabase-setup.sql` : creates the database table (already run)
- `README.md` : these notes (optional, not needed to run the site)

## Put it online (GitHub Pages)
1. Create a GitHub repository. Upload `index.html`.
2. Repository **Settings > Pages**. Under **Branch**, choose `main` and `/ (root)`, then Save.
3. After about a minute the link is `https://YOUR-NAME.github.io/REPO-NAME/`.

## Using it
- Tap the orange **DEMO DATA · 108 bins** text 7 times to open the hidden **Manage** page.
- Bins 1–108: edit name, code and quantity, then Save changes.
- Upload stock: choose a CSV or Excel file with columns Bin, Code, Name, Qty.
- Room names: rename the rooms and storage areas.

## Database
- Online database: Supabase, table `kv`.
- Settings are in `index.html`, on the line starting `window.WH_CONFIG=`.
- Only the public (publishable) key goes in this file. Never use the `sb_secret_` key.

## Important
Anyone who has the website link can change the data. Share the link only with your team.
