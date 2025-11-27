# P-Layer User Manual

**P-Layer** Free broadcast automation for small FM stations, community radio, student & hospital radio, and hobby internet stations — now on macOS

![Screenshot](screen1.png)

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/G2G01P2DJA)
---

## 1. Quick Start & Settings

Before you begin, configure the application by clicking the **Settings** button in the left sidebar.

### General Tab
*   **Playlist Folder:** Click "Select Playlist Folder" to choose the directory where your playlists will be stored. This is critical for the **Scheduler** to function.
*   **Crossfade duration:** The duration of the smooth transition between tracks (in seconds).
*   **Smart Crossfade:**
    *   *Silence Threshold:* The volume level considered as silence.
    *   *Silence Window:* How long silence must persist to trigger a transition.
    *   *Smart Crossfade only in last (sec):* Restricts smart transitions to the end of the track to prevent false positives during quiet parts of a song.
*   **Compressor mode:** Audio processing mode (Soft, Punchy, or Off). "Punchy" is recommended for a radio-like sound.

### Categories Tab (Mandatory)
To use the **Library**, you must configure at least one category.
1.  Enter a **Category Name** (e.g., "Music", "Jingles").
2.  Select a **Color** from the palette.
3.  Click **Select Folder** to choose the directory on your computer containing your audio files for this category.
4.  Click the **Checkmark (✔)** button to save.
*The files from this folder will now appear in the "Library" panel under the "Files" tab.*

> **Tip:** It is recommended to create one main folder for your music base (e.g., "P-Layer Music"). Inside it, create separate subfolders for each category (e.g., "Hits", "Gold", "Jingles"), and then connect these specific subfolders in the Category settings.

### Streaming Tab
Enter your Icecast or Shoutcast server details here:
*   **Enable streaming:** Master switch to allow broadcasting.
*   **Server Settings:** Host, Port, Mountpoint, Password, etc.
*   Once configured, the application is ready to broadcast.

---

## 2. Library & Playlist Management

### Library
The right-side panel contains your library with two tabs (switchable at the top):
1.  **Files:** Displays your audio files sorted by categories (folders). Use the search bar to filter tracks.
2.  **Commands:** A list of automation commands (see "Automation Commands" below).

### Playlist Control
*   **Add:** Drag and drop tracks from the **Library** panel OR directly from your computer's file manager (Finder/Explorer) into the central playlist area.
    *   *Note:* Tracks dropped from Finder will appear gray (uncategorized). To use color coding and rotation features properly, it is recommended to add your folders to **Settings -> Categories** and use the Library.
*   **Sort:** Drag items within the list to reorder them.
*   **Remove:** Click the `✖` button on a track card.
*   **Clear:** The **Clear Playlist** button in the menu removes all tracks from the queue.

### Timers & Indicators
*   **Queue Duration:** When the player is stopped (preparation mode), the *total duration of the queue* is displayed under the control buttons. It updates instantly when changes are made. This timer is hidden during playback.
*   **AirTime:** Each track card displays its calculated air time based on the current queue.

### Technical Requirements
*   **Supported Formats:** MP3, WAV, FLAC, M4A.
*   **Sample Rate:** **44.1 kHz** is highly recommended.
    *   *Note:* If a track has a different sample rate (e.g., 48 kHz), a warning badge (⚠️) will appear next to it in the Library. It is advised to convert such files to 44.1 kHz to ensure stable streaming.

> **Pro Tip:** Before adding tracks to your library, prepare them: **normalize loudness** (e.g., to -1 dB peak), check the sample rate, and **trim silence** at the start and end of the file for perfect transitions.

---

## 3. Automation Commands

P-Layer supports special playlist items called **Commands**. They look like tracks with a monospace font and a special icon but have zero duration.

**Available Commands:**
1.  **Start Stream:** Connects to the streaming server.
2.  **Stop Stream:** Disconnects from the server.

**How to use:**
1.  Switch to the **Commands** tab in the Library.
2.  Drag a command into the playlist just like a normal track.
3.  **Behavior:** When the playback queue reaches a command, the player executes the action (e.g., starts streaming) and **immediately** transitions to the next track.

*Example:* Place `Start Stream` as the first item to start broadcasting automatically. Place `Stop Stream` at the end to finish the show.

> **Note:** Commands are fully saved within `.m3u` playlist files. You can insert them into playlists scheduled for future dates/times (e.g., start the stream automatically at 08:00 AM tomorrow by placing a command at the top of `2025-11-25_08-00.m3u`).

---

## 4. Scheduler

The application features a built-in auto-scheduler that checks for playlists every 10 seconds.

### Scheduling a Playlist
1.  Build your playlist.
2.  Click **Save playlist**.
3.  The app suggests a filename in the format: `YYYY-MM-DD_HH-MM.m3u` (Year-Month-Day_Hour-Minute) matching the current time.
4.  Edit the date and time in the filename to match when you want this playlist to air (e.g., `2025-11-24_14-00.m3u` for tomorrow at 2:00 PM).
5.  Save the file.

### Auto-Loading Logic
*   When the system time matches the filename (down to the minute), P-Layer loads the playlist.
*   **Seamless Transition:**
    *   If music is playing: The current queue is replaced, and a smooth crossfade occurs from the *currently playing track* to the *first track of the new playlist*. No silence.
    *   If stopped: The playlist loads and starts playing automatically.

---

## 5. On-Air Control

*   **Player Controls:** Play, Pause, Next, Eject (Stop & Reset).
*   **STREAM Button:** Located below the progress bar on the right.
    *   Displays status: `STREAM OFF`, `CONNECTING...`, `STREAM ON`, `STREAM ERROR`.
    *   Clicking it allows manual toggling of the stream (if not managed by commands).

---

### Technical Notes
*   **Keep-Alive:** The audio engine generates a silent carrier signal to keep the connection alive even during silence (between a command and a track), preventing server disconnects.
*   **Loudness:** The streaming output is automatically normalized (Master Gain -2.5dB) to ensure safe headroom and professional loudness levels.

---


📡 Follow P-Layer on X: [@p_layer_app](https://x.com/p_layer_app)


---

# Руководство пользователя P-Layer (Russian)

**P-Layer** — это профессиональное приложение для автоматизации эфирного вещания. Оно позволяет создавать плейлисты, планировать выход эфиров по времени и управлять потоковым вещанием (Icecast/Shoutcast).

---

## 1. Быстрый старт и Настройка

Перед началом работы необходимо настроить приложение. Нажмите кнопку **Settings** в левом меню.

### Вкладка General (Общие)
*   **Playlist Folder:** Нажмите "Select Playlist Folder", чтобы выбрать папку, где будут храниться ваши плейлисты. Это критически важно для работы **Планировщика**.
*   **Crossfade duration:** Длительность плавного перехода между треками (в секундах).
*   **Smart Crossfade (Интеллектуальный переход):**
    *   *Silence Threshold:* Уровень громкости, который считается тишиной.
    *   *Silence Window:* Сколько времени должна длиться тишина, чтобы сработал переход.
    *   *Smart Crossfade only in last (sec):* Функция активна только в конце трека (защита от ложных срабатываний в паузах внутри песни).
*   **Compressor mode:** Режим обработки звука (Soft, Punchy или Off). Рекомендуется "Punchy" для радио-звучания.

### Вкладка Categories (Категории)
Для работы **Библиотеки** необходимо создать хотя бы одну категорию.
1.  Введите **Имя категории** (например, "Music", "Jingles").
2.  Выберите **Цвет** из палитры.
3.  Нажмите **Select Folder**, чтобы выбрать папку с аудиофайлами на вашем компьютере.
4.  Нажмите кнопку **Галочка (✔)** для сохранения.
*Файлы из этой папки появятся в панели "Library" во вкладке "Files".*

> **Совет:** Рекомендуется создать одну общую папку для музыкальной базы (например, "P-Layer Music"). Внутри нее создайте отдельные подпапки для каждой категории (например, "Хиты", "Золотые", "Джинглы") и подключайте в настройках именно эти подпапки.

### Вкладка Streaming (Вещание)
Здесь вводятся данные вашего Icecast или Shoutcast сервера:
*   **Enable streaming:** Разрешить вещание (глобальный переключатель).
*   **Server Settings:** Host, Port, Mountpoint, Password и др.
*   После ввода данных приложение готово к эфиру.

---

## 2. Работа с Библиотекой и Плейлистом

### Библиотека (Library)
Справа находится панель библиотеки. В ней есть две вкладки (переключаются сверху):
1.  **Files:** Отображает ваши аудиофайлы, отсортированные по категориям (папкам). Используйте строку поиска для фильтрации.
2.  **Commands:** Список команд автоматизации (см. раздел "Команды").

### Управление плейлистом
*   **Добавление:** Перетащите треки из панели **Library** ИЛИ прямо из папки на вашем компьютере (Finder/Проводник) в центральную область плейлиста.
    *   *Важно:* Треки, добавленные из Finder, будут отображаться серым цветом (без категории). Чтобы использовать цветовую маркировку и функции ротации, рекомендуется добавить папки через **Settings -> Categories** и использовать Библиотеку.
*   **Сортировка:** Вы можете менять порядок треков перетаскиванием внутри списка.
*   **Удаление:** Нажмите крестик `✖` на карточке трека.
*   **Очистка:** Кнопка **Clear Playlist** в меню удаляет все треки из очереди.

### Таймеры и Индикация
*   **Queue Duration:** Когда плеер остановлен (режим подготовки), под кнопками управления отображается *общая длительность очереди*. Она пересчитывается мгновенно при любых изменениях. При запуске эфира этот таймер скрывается.
*   **AirTime:** В каждой карточке трека отображается расчетное время выхода в эфир.

### Технические требования
*   **Поддерживаемые форматы:** MP3, WAV, FLAC, M4A.
*   **Частота дискретизации:** Рекомендуется **44.1 kHz**.
    *   *Важно:* Если частота трека отличается от 44.1 kHz (например, 48 kHz), в Библиотеке рядом с ним появится значок предупреждения (⚠️). Рекомендуется перекодировать такие файлы в 44.1 kHz для стабильного вещания.

> **Совет профессионала:** Перед добавлением музыки в базу подготовьте файлы: **нормализуйте громкость** (например, до -1 dB), проверьте частоту и **обрежьте тишину** в начале и конце трека. Это обеспечит идеальные переходы в эфире.

---

## 3. Команды Автоматизации (Commands)

P-Layer поддерживает специальные элементы плейлиста — **Команды**. Они выглядят как треки с моноширинным шрифтом и иконкой, но имеют нулевую длительность.

**Доступные команды:**
1.  **Start Stream:** Подключается к серверу вещания.
2.  **Stop Stream:** Разрывает соединение с сервером.

**Как использовать:**
1.  Перейдите во вкладку **Commands** в библиотеке.
2.  Перетащите команду в плейлист так же, как обычный трек.
3.  **Логика работы:** Когда очередь воспроизведения доходит до команды, плеер выполняет действие (например, включает стрим) и **мгновенно** переходит к следующему треку.

*Пример:* Поставьте команду `Start Stream` первым элементам плейлиста, чтобы эфир начался автоматически с первым треком. Поставьте `Stop Stream` в конце, чтобы завершить вещание.

> **Важно:** Команды сохраняются внутри файлов плейлистов (`.m3u`). Вы можете использовать их при планировании эфиров на будущее (например, чтобы стрим сам включился завтра в 08:00, добавьте команду в начало плейлиста `2025-11-25_08-00.m3u`).

---

## 4. Планировщик (Scheduler)

Приложение имеет встроенный автоматический планировщик, который проверяет расписание каждые 10 секунд.

### Создание расписания
1.  Соберите плейлист.
2.  Нажмите кнопку **Save playlist**.
3.  Приложение автоматически предложит имя файла в формате: `YYYY-MM-DD_HH-MM.m3u` (Год-Месяц-День_Час-Минута), соответствующее текущему времени.
4.  Измените дату и время в имени файла на то, когда этот плейлист должен выйти в эфир (например, `2025-11-24_14-00.m3u` для эфира завтра в 14:00).
5.  Сохраните файл.

### Как работает авто-загрузка
*   Когда наступает указанное время (с точностью до минуты), P-Layer находит файл.
*   **Бесшовный переход:**
    *   Если музыка играет: текущий плейлист заменяется новым, и происходит плавный кроссфейд с *текущего играющего трека* на *первый трек нового плейлиста*. Эфир не прерывается.
    *   Если плеер стоял: новый плейлист загружается и запускается автоматически.

---

## 5. Управление Эфиром

*   **Кнопки плеера:** Play, Pause, Next (следующий трек), Eject (полная остановка и сброс).
*   **STREAM кнопка:** Находится справа под прогресс-баром.
    *   Показывает статус: `STREAM OFF`, `CONNECTING...`, `STREAM ON`, `STREAM ERROR`.
    *   Нажатие на кнопку позволяет включить/выключить вещание вручную (если оно не управляется командами).

---

### Примечания
*   Для стабильного вещания даже в моменты тишины (между командой и треком) движок поддерживает "несущий сигнал" (Keep-Alive), предотвращая обрывы связи с сервером.
*   Уровень громкости вещания автоматически нормализуется (Master Gain -2.5dB), чтобы избежать перегрузки сигнала на стороне сервера.
