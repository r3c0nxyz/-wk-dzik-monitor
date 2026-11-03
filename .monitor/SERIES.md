# Seria WK DZIK

Komenda w rozmowie z ChatGPT: **rozpocznij serię**.

Na tę komendę asystent uruchamia istniejący workflow `.github/workflows/wk-dzik.yml` na `main`, przez `workflow_dispatch` z inputem `mode: series`. W UI: Actions → WK DZIK - monitor promocji → Run workflow → mode: series.

Alternatywa przez dostępne API repozytorium: odczytaj aktualny SHA `.monitor/check-request.json`, zastąp plik nowym JSON z `mode: series`, `request: rozpocznij serię`, unikalnym `requested_at` i zatwierdź zmianę na domyślnej gałęzi. To wywołuje monitor przez push. Wybierz jeden sposób; nie uruchamiaj obu, aby nie dodać dwóch serii do kolejki.

Sprawdzaj status nowego uruchomienia. Nie deklaruj startu przed potwierdzeniem wykonania; GitHub może opóźnić start lub ustawić go w kolejce. 30 minut liczy się od faktycznego rozpoczęcia pętli. Ustawienia concurrency zapobiegają równoległemu nadpisywaniu stanu.

Seria wykonuje 15 odczytów: natychmiast oraz po 2, 4, …, 28 minutach. Po 30 minutach wysyła zakończenie. Każdy odczyt wysyła wynik na skonfigurowany Telegram, także bez zmian. Zmiany zachowują nazwę i link produktu, zapis techniczny i wyjaśnienie. Bardzo opóźnione odczyty są pomijane, zamiast wykonywania zaległych w szybkiej serii. Błąd wysyłki zatrzymuje workflow; nie potwierdzaj dostarczenia, jeśli workflow zgłasza błąd.

Komenda jest obsługiwana przez asystenta w rozmowie, nie przez Telegram (bot nie odczytuje wiadomości Telegrama). Samo dodanie tej funkcji nie uruchamia serii. Zwykłe i zaplanowane uruchomienia nadal wykonują pojedynczy odczyt. Monitor zachowuje dotychczasową datę zakończenia: 30 listopada 2026.
