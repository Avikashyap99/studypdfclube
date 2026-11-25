# StudyPDFClub.in starter

A secure full-stack starter for Classes 8, 9 and 10 with:
- Student registration/login using mobile number + password (no OTP)
- Admin-only PDF upload and subject/class management
- ₹354/month Razorpay subscription flow
- Webhook-based subscription status updates

## Important
This is a starter implementation, not a production deployment. Before accepting real payments:
1. Set strong secrets and HTTPS.
2. Configure Razorpay live keys and webhook secret in the backend environment.
3. Create a Razorpay plan for ₹354 monthly and set `RAZORPAY_PLAN_ID`.
4. Deploy the API and frontend; configure the webhook URL as `https://YOUR_API_DOMAIN/api/payments/webhook`.
5. Test with Razorpay test mode first.

## Stack
- Backend: Node.js, Express, Prisma, PostgreSQL, bcrypt, JWT
- Frontend: React + Vite
- PDF files: local uploads for development. For production, use private object storage (S3-compatible) and signed downloads.

## Run locally
### Backend
```bash
cd server
cp .env.example .env
npm install
npx prisma migrate dev --name init
npm run dev
```
Create an admin by setting `ADMIN_MOBILE` and `ADMIN_PASSWORD` in `.env`, then run:
```bash
npm run seed:admin
```

### Frontend
```bash
cd client
npm install
cp .env.example .env
npm run dev
```

Frontend expects backend at `http://localhost:4000`.

## Subject structure
- Class 8: Science, Mathematics
- Class 9: Science, Mathematics
- Class 10: Science, Mathematics

## Security notes
- Passwords are hashed with bcrypt.
- Admin role is checked on every admin endpoint.
- Razorpay signature is verified server-side.
- Subscription activation/renewal/cancellation is updated by verified webhooks, not by the browser success page.
- Do not expose API secrets in frontend code.
- Add rate limiting, backups, malware scanning, audit logs and private storage before production.
