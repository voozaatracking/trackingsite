[README.md](https://github.com/user-attachments/files/25082481/README.md)
# VooZaa Device Tracking System

Ein Tracking-System für VooZaa Geräte mit Umsatzverwaltung, Mitarbeiter-Dashboard und Berichtsfunktionen.

## Features

- 📊 Dashboard mit KPIs und Monatsübersicht
- 🔍 Datenbank-Suche
- 👥 Mitarbeiter-Dashboard mit Provisionsberechnung
- 📥 Umsatz-Import (addiert automatisch)
- 📄 PDF-Berichte
- 🔐 Passwortschutz
- 💾 Persistente Datenspeicherung

## Deployment auf Vercel

### Schritt 1: Repository erstellen

1. Gehe zu [github.com/new](https://github.com/new)
2. Erstelle ein neues Repository (z.B. `voozaa-tracker`)
3. Lade diesen Code hoch:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/DEIN-USERNAME/voozaa-tracker.git
git push -u origin main
```

### Schritt 2: Vercel verbinden

1. Gehe zu [vercel.com](https://vercel.com)
2. Klicke "Add New" → "Project"
3. Importiere dein GitHub Repository
4. **Wichtig:** Füge die Environment Variables hinzu:

   | Name | Wert |
   |------|------|
   | `APP_PASSWORD` | Dein gewünschtes Passwort |

5. Klicke "Deploy"

### Schritt 3: (Optional) Supabase für persistente Daten

Ohne Supabase werden Daten im Browser-LocalStorage gespeichert (funktioniert, aber nicht geräteübergreifend).

Für persistente Daten:

1. Gehe zu [supabase.com](https://supabase.com)
2. Erstelle ein kostenloses Projekt
3. Gehe zu SQL Editor und führe aus:

```sql
CREATE TABLE app_data (
  key TEXT PRIMARY KEY,
  value TEXT,
  updated_at TIMESTAMP WITH TIME ZONE DEFAULT NOW()
);

-- Enable Row Level Security
ALTER TABLE app_data ENABLE ROW LEVEL SECURITY;

-- Allow all operations for now (einfache Variante)
CREATE POLICY "Allow all" ON app_data FOR ALL USING (true);
```

4. Kopiere aus Settings → API:
   - Project URL
   - anon public key

5. Füge in Vercel hinzu:
   | Name | Wert |
   |------|------|
   | `NEXT_PUBLIC_SUPABASE_URL` | Deine Project URL |
   | `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Dein anon key |

6. Redeploy in Vercel

## Lokale Entwicklung

```bash
npm install
npm run dev
```

Öffne [http://localhost:3000](http://localhost:3000)

## Passwort ändern

1. Gehe zu Vercel → Dein Projekt → Settings → Environment Variables
2. Ändere `APP_PASSWORD`
3. Redeploy (Deployments → ... → Redeploy)

## Support

Bei Fragen oder Änderungswünschen einfach melden!
