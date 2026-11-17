# 3D Smart Warehouse – update and Supabase setup

## Files
- `index (1)(1).html` – updated warehouse application.
- `supabase-setup.sql` – database tables, access policies, and atomic stock functions.

## 1. Update the website
Replace the old HTML file on your hosting service with the updated `index (1)(1).html`. Keep a copy of the old file before replacing it.

## 2. Set up Supabase
1. Open the correct Supabase project.
2. Open **SQL Editor**.
3. Open `supabase-setup.sql`, copy all its contents, paste into SQL Editor, and run it.
4. In **Authentication → Providers**, make sure Email sign-in is enabled.
5. In **Authentication → Users**, create the accounts that will use the warehouse. The app does not provide public self-registration.

## 3. Give Admin access
After creating the intended Admin account, copy its User UID from Authentication → Users. In SQL Editor run this, replacing the UID:

```sql
insert into public.profiles (id, role)
values ('PASTE-ADMIN-USER-UID-HERE', 'admin')
on conflict (id) do update set role = 'admin';
```

For ordinary view-only users, create a profile with role `viewer`:

```sql
insert into public.profiles (id, role)
values ('PASTE-VIEWER-USER-UID-HERE', 'viewer')
on conflict (id) do update set role = 'viewer';
```

Users sign in using the **Sign in** button in the app. Admins see editing and management controls. Viewers can sign in and view warehouse data but cannot write to the database.

## 4. Important security notes
- The browser app must use the Supabase **publishable/anon key** only. Never put a `service_role` or secret key in the HTML file.
- The database policies are the actual security boundary. Hiding buttons in the browser is not security by itself.
- The SQL creates `public.kv` with a primary key on `(coll, id)`, and the app expects those exact column names.
- Atomic bin edits and stock moves require the SQL functions in the supplied script. Do not remove them.
- Keep backups of the existing database before applying schema changes to a live warehouse.

## 5. First use / verification
1. Open the updated website while connected to the internet.
2. Sign in as the Admin account.
3. Check that the status near the title says **Admin · shared database**.
4. Add a test material to an unused bin, reload the page, and confirm it remains.
5. Sign in as a viewer in a separate browser/device and confirm editing controls are not shown and database writes are rejected by RLS.
6. Test stock-in, issue, move, area changes, room names, CSV/Excel preview, and history with test data before using live stock.

## Notes about this update
The updated source passes JavaScript syntax validation. It has not been authenticated against your live Supabase project or tested with your actual warehouse users/devices. Existing rows in a compatible `kv` table are retained; the app does not automatically delete or reset existing warehouse data. Take a database backup before running the SQL on a production project.
