# הרצה מקומית עם Docker Desktop

המדריך הזה מרים את כל המערכת על המחשב שלך: מסד נתונים, השרת, האתר, אחסון קבצים ומסך לצפייה במסד הנתונים.
בגרסה המקומית אין צורך בהתחברות, והקבצים נשמרים במחשב ולא באמזון.

## מה צריך מראש

- **Docker Desktop**, פתוח ורץ (סמל הלוויתן בשורת המשימות).
- **Git**, מ-https://git-scm.com/download/win (התקנה עם ברירות המחדל).

## התקנה (פעם אחת)

פותחים **PowerShell** ומריצים, שורה אחרי שורה:

```powershell
mkdir C:\calculaud
cd C:\calculaud
git clone -b local-setup https://github.com/eliya6002-beep/calculaud-be.git
git clone https://github.com/eliya6002-beep/calculaud-fe.git
cd calculaud-be
docker compose up -d --build
```

ההרצה הראשונה לוקחת כמה דקות, כי Docker מוריד את כל מה שצריך.

## מילוי נתוני דוגמה (פעם אחת)

```powershell
docker compose exec api python -m scripts.seeder.main
```

זה ממלא את המערכת בספקים, מחלקות ודרישות רכש לדוגמה, כדי שיהיה מה לראות.

## הכתובות

| מה | כתובת |
| --- | --- |
| האתר | http://localhost:8080 |
| השרת (תיעוד ה-API) | http://localhost:8000/docs |
| צפייה במסד הנתונים | http://localhost:8081 (מערכת PostgreSQL, שרת `db`, משתמש `calculaud`, סיסמה `calculaud`, מסד `calculaud`) |
| אחסון הקבצים | http://localhost:9001 (משתמש `calculaud`, סיסמה `calculaud-local`) |

האתר עולה רק אחרי שהתקנת החבילות שלו מסתיימת. אם הכתובת לא נפתחת מיד, מחכים דקה ומרעננים.

## שימוש יומיומי

כל הפקודות רצות מתוך התיקייה `C:\calculaud\calculaud-be`.

| רוצה | פקודה |
| --- | --- |
| להפעיל | `docker compose up -d` |
| לעצור | `docker compose down` |
| לראות מה רץ | `docker compose ps` |
| לראות הודעות של השרת | `docker compose logs -f api` |
| לראות הודעות של האתר | `docker compose logs -f web` |
| למחוק הכול ולהתחיל מאפס | `docker compose down -v` |

שינוי בקוד מתעדכן לבד, בלי להפעיל מחדש.

## אם משהו לא עובד

- **"docker" לא מזוהה:** Docker Desktop לא פתוח. פותחים אותו ומחכים שיסיים לעלות.
- **פורט תפוס (port is already allocated):** תוכנה אחרת במחשב משתמשת באחד הפורטים 5432, 8000, 8080, 8081, 9000 או 9001. סוגרים אותה, או משנים את המספר הראשון בשורה המתאימה ב-`docker-compose.yml`.
- **האתר פתוח אבל אין נתונים:** מריצים את פקודת מילוי הנתונים שלמעלה.
