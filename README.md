# Fanlar boti

Telegram bot + mini app: fan → sinf (6–11) → mavzu → savol. Öquvçi savolga ovoz bilan javob beradi, Gemini AI javobni bazadagi töğri javob bilan solişadi. Savollarni faqat admin mini app içidagi "Tahrirlaş" tugmasi orqali kiritadi.

Mavzuga kirganda öquvçi rejim tanlaydi: **ovozli suhbat** (savol ovoz çiqarib öqiladi, mikrofon özi yoqiladi, natija ham ovoz bilan aytiladi) yoki **oddiy rejim** (savol matnda, javob ovoz bilan yoki yozma). Har bir savol ovozi bir marta yaratilib bazada saqlanadi.

## Tarkibi

- `main.py` — server: bot webhook, API, baza, AI tekşiruvi
- `static/index.html` — mini app va admin panel
- `Dockerfile` — Railway şu fayl böyiça quradi

## Railway özgaruvçilari (Variables)

| Nomi | Qiymati |
|---|---|
| `BOT_TOKEN` | @BotFather bergan token |
| `GEMINI_API_KEY` | aistudio.google.com/apikey dan olingan kalit |
| `ADMIN_IDS` | Admin Telegram ID raqami (bir neçta bölsa vergul bilan). Botga `/id` yozsangiz körsatadi |
| `DATABASE_URL` | `${{Postgres.DATABASE_URL}}` |
| `GEMINI_MODEL` | Ixtiyoriy. Standart: `gemini-flash-latest` |
| `GEMINI_TTS_MODEL` | Ixtiyoriy. Savolni ovoz çiqarib öqiydigan model. Standart: `gemini-3.8-flash-tts` |
| `GEMINI_TTS_VOICE` | Ixtiyoriy. Ovoz nomi. Standart: `Kore` |

## Deploy

1. Şu papkadagi fayllarni GitHub repoga yuklang.
2. Railway → New Project → Deploy from GitHub repo → reponi tanlang.
3. Loyihada: + New → Database → PostgreSQL.
4. Bot servisi → Variables → yuqoridagi özgaruvçilarni kiriting.
5. Bot servisi → Settings → Networking → Generate Domain.
6. Deployments → Redeploy. Server işga tuşganda webhook va botdagi "Fanlar" menyu tugmasi özi sozlanadi.
7. Botga `/id` yozing, çiqqan raqamni `ADMIN_IDS` ga kiriting.

`DATABASE_URL` kiritilmasa, maʼlumotlar vaqtinçalik faylda saqlanadi va har deployda öçib ketadi.

## Lokal sinov

```
pip install -r requirements.txt
DEV_MODE=1 uvicorn main:app --reload
```

`DEV_MODE=1` Telegram tekşiruvisiz admin sifatida kirişga ruxsat beradi. Uni Railway'da qöymang.
