# WSA-05 - Jelszó módosítása

## Mint belépett felhasználó, szeretném megváltoztatni a jelszavam, hogy később ennek segítségével érhessem el a szolgáltatásokat

### Pontok: 1
### Szolgáltatás: [PATCH /user/login](http://localhost:5000/api-doc#/Users/AuthController_changePassword)
### Prioritás: közepes

A feladat egy form létrehozása, amin egy már belépett felhasználó módosítani tudja korábban megadott jelszavát. Csak belépett felhasználók számára érhető el, közvetlen hivatkozással történő eléréskor token hiányában irányítsuk a felhasználót a belépési oldalra.  
A felhasználó által megadott adatok kliens oldalon formailag ellenőrizzük, érvénytelen adatok nem küldhetőek a szolgaltáshoz. A régi és az új jelszó nem egyezhet meg egymással.  
Sikeres jelszó változtatás esetén jelezzük azt a felhasználó részére egy üzenet formájában.

#### Bemeneti adatok:
- Régi jelszó
  - mezőnév: oldPassword
  - típus: szöveg, jelszó
  - validáció:
    - Kötelező kitölteni
    - A jelszónak legalább 8 karakter hosszúnak kell lennie legalább 1 számmal és 1 kisbetűvel
- Új jelszó
  - mezőnév: password
  - típus: szöveg, jelszó
  - validáció:
    - Kötelező kitölteni
    - A jelszónak legalább 8 karakter hosszúnak kell lennie legalább 1 számmal és 1 kisbetűvel
- Új jelszó megerősítése
  - mezőnév: passwordConfirm
  - típus: szöveg, jelszó
  - validáció:
    - Kötelező kitölteni
    - a tartalma meg kell egyezzen az új jelszó mezővel

#### Példa bemeneti adatra:
```
{
  "oldPassword": "admin123",
  "password": "admin321",
  "passwordConfirm": "admin321"
}
```

#### Sikeres változtatás
204 No content válaszkód

#### A szolgáltatás által visszajelzett hibák:
- 400 Bad request - a bevitt adatok érvénytelenek
- 401 Unauthorized - hiányzó, vagy érvénytelen token
- 409 Conflict - a régi és az új jelszó azonos (hibás bemenet)