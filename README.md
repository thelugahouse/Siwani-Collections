# The Luga House – Siwani Collections

A free-to-host, mobile-first ecommerce storefront with a secure Supabase-backed admin panel, realtime catalogue updates and WhatsApp ordering.

## Included
- Corporate design based on the supplied gold / pink / navy logo.
- Men, Ladies, Kiddos and Accessories categories.
- Product search, sorting, category filters, wishlist and shopping bag.
- Product details and size display.
- WhatsApp checkout to **9868220779** with an automatically generated cart message.
- Admin login with Supabase Auth.
- Admin CRUD for products and categories.
- Admin social-link settings for Facebook, Instagram, YouTube, TikTok, Twitter/X and LinkedIn.
- Supabase Realtime: changes saved in the admin panel are pushed to connected storefronts automatically.
- Demo catalogue appears before Supabase is configured so the design can be previewed immediately.

## 100% free setup option
Use:
1. **Supabase Free** for database, authentication and realtime.
2. **GitHub Pages** (or another free static host) for the website.

No paid server is required for this version. Payment gateway, courier API and custom-domain fees are optional and are not required for WhatsApp ordering.

## Setup
### 1) Create Supabase
Create a free project at https://supabase.com/.

### 2) Database
Open SQL Editor and run `supabase.sql`.

If Supabase says a table is already in `supabase_realtime`, skip that duplicate `alter publication` line.

### 3) Create admin account
In Supabase: Authentication → Users → Add user. Create your admin email/password.
Copy the user's UUID, then run:

```sql
insert into public.profiles(id,role)
values ('YOUR-AUTH-USER-UUID','admin')
on conflict (id) do update set role='admin';
```

### 4) Configure the website
Open `config.js` and replace:

```js
supabaseUrl: 'YOUR_SUPABASE_URL',
supabaseAnonKey: 'YOUR_SUPABASE_ANON_KEY'
```

Use the **Project URL** and **anon/public key** from Supabase Project Settings → API. Never put a service-role key in this site.

### 5) Product images
The quickest free option is to paste image URLs into the admin panel. You can also add Supabase Storage later and use a public `product-images` bucket.

### 6) Run locally
Because browsers can restrict local files, use a tiny local server, for example VS Code Live Server, or:

```bash
python -m http.server 8080
```

Then open `http://localhost:8080`.

### 7) Free deployment
Upload the folder to a GitHub repository and enable GitHub Pages. The site is static, so no paid backend server is needed. Supabase remains the live database/realtime service.

## Important production notes
- Keep RLS enabled.
- Use only the Supabase anon/public key in `config.js`.
- Admin write access is protected by `profiles.role='admin'`.
- WhatsApp number is preconfigured as Nepal number `+977 9868220779`.
- Social links are intentionally blank until you enter your official links in Admin → Settings.
- This starter intentionally does not collect card/payment details. If you later want online payments, add a Nepal-compatible payment gateway separately.
