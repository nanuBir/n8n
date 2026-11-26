# Free n8n Cloud Server (Android Mobile Setup Guide)

Is repository ki madad se aap apne Android phone se bina kisi laptop ya credit card ke **24/7 chalne wala n8n server** free mein setup kar sakte hain.

## Step 1: GitHub par Files Upload Karein
1. GitHub.com par login karein aur **New Repository** banayein (naam rakhein: `my-n8n-app`).
2. **Add file -> Upload files** par click karein aur is zip ke andar ki teeno files (`Dockerfile`, `render.yaml`, `README.md`) upload karke **Commit changes** daba dein.

## Step 2: Supabase par Free Database Banayein
1. [Supabase.com](https://supabase.com) par Google se login karein aur **New Project** banayein.
2. Database ka ek password set karein aur project banne ka 2 minute intezar karein.
3. Project khulne par upar **Connect** button par click karein -> **Session Pooler** (ya Direct Connection) ke details note karein:
   - **Host** (jaise `aws-0-ap-south-1.pooler.supabase.com`)
   - **Port** (`5432` ya `6543`)
   - **User** (jaise `postgres.xxxxxx`)
   - **Password** (jo aapne banaya tha)

## Step 3: Render.com par Deploy Karein
1. [Render.com](https://render.com) par apne GitHub account se login karein.
2. **New + -> Web Service** par click karein aur apni `my-n8n-app` repository ko **Connect** karein.
3. **Instance Type** mein **Free** select karein.
4. **Environment Variables** section mein yeh details daalein:
   - `DB_TYPE` = `postgresdb`
   - `DB_POSTGRESDB_HOST` = *(Supabase Host)*
   - `DB_POSTGRESDB_PORT` = `5432` *(ya jo port Supabase mein dikhe)*
   - `DB_POSTGRESDB_DATABASE` = `postgres`
   - `DB_POSTGRESDB_USER` = *(Supabase User)*
   - `DB_POSTGRESDB_PASSWORD` = *(Supabase Password)*
   - `DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED` = `false`
   - `N8N_ENCRYPTION_KEY` = *(Koi bhi 20-30 aksharon ka random password likh dein)*
   - `GENERIC_TIMEZONE` = `Asia/Kolkata`
5. **Deploy Web Service** par click karein. 5-7 minute mein aapka live URL (jaise `https://my-n8n-app.onrender.com`) taiyar ho jayega!

## Step 4: WEBHOOK_URL Update Karein aur App Banayein
1. Live URL milne ke baad Render ke **Environment** tab mein jakar ek aur variable add karein:
   - `WEBHOOK_URL` = *(Aapka Render URL, jaise `https://my-n8n-app.onrender.com/`)*
2. Is link ko Chrome browser mein kholein -> **3 dots -> Add to Home screen** par click karein. Aapka n8n app phone mein install ho jayega!

## Step 5: 24/7 Active Rakhne ke Liye (Optional)
Render ka free server 15 minute inactive rehne par sleep mode mein jata hai. Isse bachne ke liye [UptimeRobot.com](https://uptimerobot.com) par free account banakar apne Render URL ka HTTP monitor laga dein (har 5 minute ping ke saath).
