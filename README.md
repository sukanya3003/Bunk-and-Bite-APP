# Bunk and Bite 🍛
Android app (Kotlin + Jetpack Compose) + Node.js/Express/SQLite backend.
Pre-order food, pay by UPI, get a pickup QR/token, play music, and request songs on the restaurant jukebox.

```
BunkAndBite/
├─ app/      Android app
└─ server/   Node.js API (SQLite database - nothing to install or configure)
```

## 1. Start the server (do this FIRST, and keep it running)
Requires Node.js 18+.
```bash
cd server
npm install
npm start
```
You should see `Bunk and Bite API running on http://localhost:5000`.
On the first start it creates `database.sqlite` and seeds 56 menu items, 8 songs and demo logins.
No `.env` file is required. (Optional: copy `.env.example` to `.env` to change the UPI id / secret.)

Quick check: open http://localhost:5000/api/menu in your browser - you should see JSON.
Food pictures live in `server/public/images/` - replace any file (same name) with a real photo.

## 2. Run the app on the emulator
1. Android Studio -> **Open** the `BunkAndBite` folder (not `server`) -> wait for Gradle sync.
2. Device Manager -> create a Pixel emulator (API 34, "Google APIs" image) -> press **Run**.
3. The app reaches your computer's server at `http://10.0.2.2:5000/` (the emulator's alias for
   `localhost`). On a **real phone**, change `BASE_URL` in
   `app/src/main/java/com/example/canteen/network/RetrofitClient.kt` to your PC's Wi-Fi IP.

## Logins
| Role     | Email               | Password  |
|----------|---------------------|-----------|
| Chef     | chef@canteen.com    | chef123   |
| Admin    | admin@canteen.com   | admin123  |
| Customer | tap "Create an account" in the app |

## Troubleshooting
- **"Can't reach the server"** -> the server isn't running (step 1), or you're on a real phone with the emulator URL.
- **"No account with this email"** -> use *Create an account* first (or a demo login above).
- **Fresh database** -> stop the server, delete `server/database.sqlite`, start again
  (or run `npm run seed`, which wipes and reseeds).
- **Payment on emulator** -> there is no UPI app, so the app offers *Simulate payment* - tap it to continue.
