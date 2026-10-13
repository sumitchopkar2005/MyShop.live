# My-Shop — SaaS Personal Website Builder

A full-stack SaaS platform where users can create premium personal portfolio websites (digital business cards) and share them via a unique public URL.

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Next.js 15, Tailwind CSS, GSAP animations |
| **Backend** | Node.js, Express.js |
| **Database** | MongoDB (Mongoose ODM) |
| **Auth** | JWT (JSON Web Tokens) |
| **File Storage** | Cloudinary |
| **UI** | Glassmorphism, Gradient buttons, Mobile-first |

---

## Project Structure

```
saaswebsite/
├── backend/                  # Express API
│   ├── src/
│   │   ├── controllers/      # authController, websiteController, adminController...
│   │   ├── middleware/        # auth.js (JWT), upload.js (multer)
│   │   ├── models/           # User.js, Website.js, Visit.js
│   │   ├── routes/           # auth, website, admin, public, upload
│   │   ├── utils/            # cloudinary.js, seed.js
│   │   └── server.js
│   ├── .env.example
│   └── package.json
│
└── frontend/                 # Next.js App
    ├── app/
    │   ├── page.js           # Landing page
    │   ├── login/            # Login page
    │   ├── signup/           # Signup page
    │   ├── dashboard/        # User dashboard
    │   │   ├── page.js       # Overview
    │   │   ├── editor/       # Website editor (all sections)
    │   │   ├── preview/      # Live preview
    │   │   ├── analytics/    # Visit analytics
    │   │   └── settings/     # Profile & password
    │   ├── admin/            # Admin panel
    │   │   ├── page.js       # Stats overview
    │   │   ├── users/        # Manage users
    │   │   └── websites/     # Manage websites
    │   └── [username]/       # 🌐 Public profile page
    ├── components/
    │   └── public/ContactForm.js
    ├── lib/
    │   ├── api.js            # Axios API client
    │   └── store.js          # Zustand auth store
    └── package.json
```

---

## Features

### User Auth
- Signup with unique username
- Login with JWT
- Change password / update profile

### Dashboard
- Overview with stats and public URL
- Full website editor with sections:
  - Hero (name, photo, tagline, CTA)
  - About (bio, skills, experience, education)
  - Services (icon, title, description, price)
  - Portfolio / Gallery (drag-and-drop uploads)
  - Products (image, price, buy link)
  - Contact (phone, WhatsApp, email, address, Google Maps embed)
  - Social media links
  - Payment QR code
  - SEO settings (title, meta description, OG image)
  - Theme color customisation
- One-click publish / unpublish
- QR code generator for sharing
- Live preview (desktop + mobile)
- Visit analytics with bar chart

### Public Profile (`/username`)
- Beautiful GSAP-animated portfolio page
- Dynamic theme colors per user
- Multi-tenant host routing support:
  - Path tenant: `yoursite.com/username`
  - Subdomain tenant: `username.yoursite.com`
  - Custom domain tenant: `links.theirbrand.com`
- Floating WhatsApp button
- Sticky mobile contact bar (Call / WhatsApp / Email)
- Contact form
- Social media links
- Google Maps embed
- Payment QR section
- Scroll-to-top button
- SEO meta tags

### Admin Panel
- Dashboard with platform-wide stats
- User management (enable/disable)
- Website management (enable/disable, view)
- Top visited websites

---

## Getting Started

### Prerequisites
- Node.js 18+
- MongoDB (local or Atlas)
- Cloudinary account (free tier works)

---

### 1. Backend Setup

```bash
cd backend
npm install
```

Copy and configure environment variables:
```bash
cp .env.example .env
```

Edit `.env`:
```env
NODE_ENV=development
PORT=5000
MONGODB_URI=mongodb://localhost:27017/saaswebsite
JWT_SECRET=your_super_secret_32_char_key_here
JWT_EXPIRES_IN=7d
FRONTEND_URL=http://localhost:3000
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
```

Start the backend:
```bash
npm run dev
```

Seed admin user:
```bash
npm run seed
# Admin credentials: admin@saaswebsite.com / Admin@1234
```

---

### 2. Frontend Setup

```bash
cd frontend
npm install
```

Copy and configure environment variables:
```bash
cp .env.local.example .env.local
```

Edit `.env.local`:
```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

Start the frontend:
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

---

## API Routes

### Auth
| Method | Route | Description |
|---|---|---|
| POST | `/api/auth/signup` | Register new user |
| POST | `/api/auth/login` | Login |
| GET | `/api/auth/me` | Get current user |
| PUT | `/api/auth/update-profile` | Update profile |
| PUT | `/api/auth/change-password` | Change password |

### Website
| Method | Route | Description |
|---|---|---|
| GET | `/api/website/me` | Get my website |
| PUT | `/api/website/me` | Update website |
| POST | `/api/website/me/publish` | Toggle publish |
| GET | `/api/website/me/qr` | Generate QR code |
| GET | `/api/website/me/analytics` | Get analytics |

### Upload
| Method | Route | Description |
|---|---|---|
| POST | `/api/upload/profile-image` | Upload profile photo |
| POST | `/api/upload/gallery` | Upload gallery image |
| DELETE | `/api/upload/gallery/:publicId` | Delete gallery image |
| POST | `/api/upload/product-image` | Upload product image |
| POST | `/api/upload/payment-qr` | Upload QR image |

### Public
| Method | Route | Description |
|---|---|---|
| GET | `/api/public/resolve-host?host=example.com` | Resolve tenant username from subdomain/custom domain |
| GET | `/api/public/:username` | Get public website (tracks visit) |
| GET | `/api/public/check/:username` | Check username availability |

### Admin (admin only)
| Method | Route | Description |
|---|---|---|
| GET | `/api/admin/stats` | Platform stats |
| GET | `/api/admin/users` | List users |
| PUT | `/api/admin/users/:id/toggle-status` | Enable/disable user |
| GET | `/api/admin/websites` | List websites |
| PUT | `/api/admin/websites/:id/toggle-disable` | Enable/disable website |

---

## Deployment

### Backend → Railway / Render / Fly.io
Set all environment variables in the hosting platform's dashboard.

Required for host-based tenant routing:
- `ROOT_DOMAIN=yourdomain.com`
- `RESERVED_SUBDOMAINS=www,app,admin,api`

### Frontend → Vercel
```bash
cd frontend
vercel --prod
```
Set `NEXT_PUBLIC_API_URL` and `NEXT_PUBLIC_SITE_URL` in Vercel project settings.

#### Vercel Subdomains + Custom Domains
1. Add wildcard domain to frontend project: `*.yourdomain.com`.
2. Add root/apex domain as well: `yourdomain.com`.
3. Add each customer custom domain to the same Vercel project.
4. Point customer DNS CNAME to your Vercel target.
5. Middleware resolves hostname using `/api/public/resolve-host` and rewrites `/` to `/:username`.

#### Nginx Example (if self-hosting frontend)
```nginx
server {
  listen 80;
  server_name yourdomain.com *.yourdomain.com;

  location / {
    proxy_pass http://127.0.0.1:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-Host $host;
    proxy_set_header X-Forwarded-Proto $scheme;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
}
```

For user custom domains, add them to `server_name` (or use dynamic certificate tooling) and keep forwarding original `Host` header.

### Database → MongoDB Atlas
Replace `MONGODB_URI` with your Atlas connection string.

---

## License
MIT
