Jasne, K — i powiem Ci od razu: **to, co widziałeś na liście Build Action, to miks opcji z .NET, MAUI, Androida i narzędzi deweloperskich**. Nic dziwnego, że to wygląda jak chaos. Seniorzy też często nie wiedzą, co połowa z nich robi, bo większość jest używana tylko w bardzo specyficznych scenariuszach.

Zrobię Ci **najbardziej praktyczne, senior‑friendly wyjaśnienie**, bez lania wody — tylko to, co realnie musisz wiedzieć.

---

# 🔥 Najważniejsze Build Action w MAUI (te, które naprawdę użyjesz)

## **1. MauiAsset**
To jest MAUI‑owy sposób na dodanie pliku do paczki aplikacji.

- Plik trafia do zasobów aplikacji (pakietu).
- Odczytujesz go przez:
  ```csharp
  using var stream = await FileSystem.OpenAppPackageFileAsync("words.txt");
  ```
- Idealne dla statycznych danych, obrazów, plików tekstowych.

👉 **To jest najprostsza opcja dla Twojego `words.txt`.**

---

## **2. Embedded resource**
Klasyczne .NET — plik trafia do DLL.

- Odczytujesz przez:
  ```csharp
  Assembly.GetManifestResourceStream("Namespace.Folder.File.txt");
  ```
- Dobre, jeśli chcesz mieć pełną kontrolę nad zasobami i nie polegać na MAUI.

👉 Bardziej „hardcore”, ale cross‑platform i przewidywalne.

---

## **3. Content**
Plik jest kopiowany do katalogu aplikacji.

- Możesz go czytać przez `File.ReadAllLines`.
- Musisz używać `FileSystem.AppDataDirectory`.

👉 Używaj, jeśli plik ma być **modyfikowany** przez aplikację.

---

## **4. None**
Plik jest ignorowany przez build.

👉 Użyteczne, jeśli chcesz mieć plik w projekcie, ale nie chcesz, żeby był w aplikacji.

---

# 🔥 Build Action MAUI‑specyficzne

## **5. MauiImage**
Dla obrazów, które mają być automatycznie skalowane i generowane na różne platformy.

## **6. MauiIcon**
Dla ikon aplikacji.

## **7. MauiSplashScreen**
Dla splash screenów.

## **8. MauiFont**
Dla czcionek.

## **9. MauiCss**
Dla CSS w Blazor Hybrid.

👉 Wszystkie te opcje automatyzują generowanie zasobów dla Android/iOS/Windows.

---

# 🔥 Android‑specyficzne (używane tylko w projekcie Android)

Te opcje pojawiają się, bo MAUI ma w sobie projekt Android:

- **AndroidAsset** — pliki w `Assets/`
- **AndroidResource** — pliki w `Resources/`
- **AndroidJavaSource** — kod Java
- **AndroidNativeLibrary** — natywne biblioteki `.so`
- **AndroidEnvironment** — zmienne środowiskowe
- **AndroidManifestOverlay** — dodatkowe manifesty
- **AndroidAotProfile** — profil AOT
- **AndroidLibrary** — biblioteki Android

👉 **W MAUI prawie nigdy ich nie używasz ręcznie.**

---

# 🔥 Narzędzia i meta‑opcje (prawie nigdy nie dotykasz)

- **C# compiler** — normalny plik .cs
- **C# analyzer additional file** — pliki dla Roslyn
- **editorconfig file** — konfiguracja stylu kodu
- **Workflow definition** — pliki workflow
- **TransformFile** — pliki transformacji
- **LinkDescription** — konfiguracja linkerów
- **ProguardConfiguration** — konfiguracja ProGuard (Android)
- **JavaDocJar / JavaDocIndex** — dokumentacja Java
- **LibraryProjectProperties** — właściwości projektu biblioteki

👉 To są rzeczy, które dotykasz tylko przy bardzo zaawansowanych projektach.

---

# 🔥 Najprostsze podsumowanie, jakie istnieje

| Build Action | Kiedy używać |
|--------------|--------------|
| **MauiAsset** | Pliki statyczne, które chcesz odczytać przez `OpenAppPackageFileAsync` |
| **Embedded resource** | Pliki wbudowane w DLL, odczyt przez `GetManifestResourceStream` |
| **Content** | Pliki, które mają być fizycznie w katalogu aplikacji |
| **None** | Plik ignorowany |
| **MauiImage / MauiIcon / MauiFont / MauiSplashScreen** | Zasoby graficzne MAUI |
| **AndroidAsset / AndroidResource** | Tylko jeśli robisz coś specyficznego dla Androida |

---

# 🔥 Chcesz, żebym zrobił Ci tabelę „co wybrać w jakiej sytuacji”?

Np.:

- „Mam plik .txt z danymi → co wybrać?”
- „Chcę, żeby użytkownik mógł edytować plik → co wybrać?”
- „Chcę, żeby plik był tylko do odczytu → co wybrać?”
- „Chcę, żeby działało na Android/iOS/Windows bez zmian → co wybrać?”

Mogę Ci to rozpisać tak, że będziesz miał gotowy wzorzec na całe życie.
